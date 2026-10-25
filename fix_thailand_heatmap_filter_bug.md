# Antigravity Bug Fix Prompt: Thailand Heatmap Category Filter Issue

## 🐛 Problem Description
ใน **TAB 1**, เมื่อผู้ใช้เลือกเปลี่ยนหมวดหมู่ปัญหาใน Dropdown Filter กราฟแผนที่ประเทศไทย (Thailand Heatmap) **ไม่แสดงผลสีใดๆ บนพื้นที่จังหวัด (กลายเป็นสีโปร่งใส/สีดำ หรือสีหายทั้งหมด)**

---

## 🔍 Root Cause Analysis (สาเหตุที่เป็นไปได้ทางเทคนิค)
1. **Type Mismatch / Parsing Failure:** ค่า `Per_vill` ถูกอ่านเป็น String แทนที่จะเป็น Float ทำให้การคำนวณ Min/Max และ Color Scale function คืนค่าเป็น `NaN` หรือ `undefined`
2. **String Mismatch:** ข้อความใน Dropdown ไม่ตรงกับค่าในคอลัมน์ `category` หรือ `Iss_Need_Grouped` ในไฟล์ CSV (เช่น มี whitespace ส่วนเกิน หรือชื่อหมวดหมู่ไม่ตรงกัน)
3. **GeoJSON Property Name Mismatch:** ชื่อจังหวัดใน CSV (`region`) ไม่ตรงกับ Property Key ของ GeoJSON/SVG (เช่น `pro_th`, `NAME_1`, `name`)
4. **Missing Fallback Color:** เมื่อจังหวัดใดไม่มีข้อมูลของหมวดหมู่ที่เลือก ระบบไม่ได้ใส่สี Fallback (เช่น `#1F1F2E`) ทำให้พื้นที่กลายเป็นสีสี่เหลี่ยมโปร่งใส
5. **Chart Redraw / State Update Failure:** ฟังก์ชัน `addEventListener('change')` ไม่ได้สั่ง Re-render หรือ Update Series Data ของแผนที่อย่างถูกต้อง

---

## 🛠️ Step-by-Step Fix Instructions for Antigravity

โปรดแก้ไขโค้ด JavaScript ในส่วนการ Render และ Filter แผนที่ประเทศไทยตามแนวทางต่อไปนี้อย่างเคร่งครัด:

### 1. Data Cleaning & Type Conversion
```javascript
// แปลงค่า Per_vill ให้เป็น Float และ Trim ชื่อหมวดหมู่/จังหวัดเสมอ
const cleanData = rawData.map(row => ({
    ...row,
    region: row.region ? row.region.trim() : '',
    category: row.category ? row.category.trim() : '',
    Iss_Need_Grouped: row.Iss_Need_Grouped ? row.Iss_Need_Grouped.trim() : '',
    Per_vill: parseFloat(row.Per_vill) || 0
}));
```

### 2. Province Name Normalization Matching
สร้าง Dictionary แปลงชื่อจังหวัดระหว่าง GeoJSON และ CSV เพื่อป้องกันปัญหานามสกุล/ชื่อไม่ตรงกัน (เช่น "กรุงเทพมหานคร" vs "กรุงเทพฯ"):
```javascript
function normalizeProvinceName(name) {
    if (!name) return '';
    let cleanName = name.trim().replace('จ.', '').replace('จังหวัด', '');
    if (cleanName === 'กรุงเทพฯ' || cleanName === 'กทม') return 'กรุงเทพมหานคร';
    return cleanName;
}
```

### 3. Dynamic Filter & Dynamic Color Scale Logic
เขียนฟังก์ชันกรองข้อมูลและคำนวณ Min/Max ของ % ความเดือดร้อนใหม่ทุกครั้งที่มีการเปลี่ยน Filter:

```javascript
function updateThailandMap(selectedCategory) {
    // 1. Filter ข้อมูลตามหมวดหมู่ที่เลือก (หากเป็น 'ALL' ให้เอาค่า Max Per_vill ของแต่ละจังหวัด)
    let filteredData = {};
    
    cleanData.forEach(row => {
        const prov = normalizeProvinceName(row.region);
        if (!prov || prov === 'ทั่วประเทศ') return;

        const isMatch = (selectedCategory === 'ALL') || 
                        (row.category === selectedCategory) || 
                        (row.Iss_Need_Grouped === selectedCategory);

        if (isMatch) {
            if (!filteredData[prov] || row.Per_vill > filteredData[prov].value) {
                filteredData[prov] = {
                    name: prov,
                    value: row.Per_vill,
                    issue: row.Iss_Need || row.Iss_Need_Grouped,
                    category: row.category
                };
            }
        }
    });

    // 2. คำนวณหาค่า Max Value เพื่อนำไปสร้าง Color Domain
    const values = Object.values(filteredData).map(d => d.value);
    const maxValue = values.length > 0 ? Math.max(...values) : 100;
    const minValue = values.length > 0 ? Math.min(...values) : 0;

    // 3. กำหนด Palette สี Neon Halloween Theme
    // น้อย -> ส้ม -> แดง -> วิกฤต (Neon Pink/Red)
    function getColor(val) {
        if (val === 0 || val === undefined) return '#1A1A24'; // Default Dark Gray for No Data
        if (val < 20) return '#FFB703'; // Yellow/Orange
        if (val < 35) return '#FB8500'; // Orange
        if (val < 50) return '#FF0055'; // Neon Pink/Red
        return '#800020'; // Dark Blood Red
    }

    // 4. Update GeoJSON/ECharts Map Series
    // ตัวอย่างสำหรับ ECharts:
    const mapSeriesData = Object.keys(filteredData).map(prov => ({
        name: prov,
        value: filteredData[prov].value,
        itemStyle: {
            areaColor: getColor(filteredData[prov].value)
        },
        extraData: filteredData[prov]
    }));

    // Re-render Chart
    myMapChart.setOption({
        visualMap: {
            min: minValue,
            max: maxValue,
            calculable: true,
            inRange: {
                color: ['#1A1A24', '#FFB703', '#FB8500', '#FF0055', '#D00000']
            },
            textStyle: { color: '#F0F0F0' }
        },
        series: [{
            type: 'map',
            map: 'thailand',
            data: mapSeriesData
        }]
    });
}
```

### 4. Event Listener Implementation
ตักเตือนให้ผูก Event Listener ของ Dropdown กับฟังก์ชัน `updateThailandMap` ให้ถูกต้อง:

```javascript
document.getElementById('mapCategoryFilter').addEventListener('change', function(e) {
    const selectedVal = e.target.value;
    updateThailandMap(selectedVal);
});
```

---

## 🎯 Expected Result After Fix
1. เมื่อเปิดหน้าแรก (Default / 'ALL'): แผนที่แสดงระดับสีส้ม-แดงตามค่าความเดือดร้อนสูงสุดของแต่ละจังหวัด
2. เมื่อเปลี่ยนฟิลเตอร์หมวดหมู่ปัญหาใน Dropdown:
   * แผนที่จะ ** Re-render สีทันที ** ตามค่า `% Per_vill` ของปัญหานั้นๆ ในแต่ละจังหวัด
   * จังหวัดที่ไม่พบปัญหานั้นจะแสดงสีเทาเข้ม `#1A1A24` (ไม่โปร่งใสหายไป)
   * Tooltip ยังคงแสดงชื่อจังหวัด และ % ความเดือดร้อนได้อย่างถูกต้อง ไม่หลุดขอบหน้าจอ
# Master Prompt for Antigravity: Halloween Dashboard (2-Tab System & 9-Group Real External Benchmark Data)

คุณคือ Senior Full-Stack Developer และ Data Visualization Expert หน้าที่ของคุณคือสร้าง/ปรับปรุง **Interactive Dashboard** แบบ Single-File (`index.html`) ธีม **Halloween** โดยใช้ข้อมูลสำรวจหลัก `data_clean_grouped_region.csv` ร่วมกับไฟล์ข้อมูลสถิติจริงจากหน่วยงานภายนอก 9 หมวดหมู่ (`group1` - `group9`)

⚠️ **ข้อกำหนดโครงสร้างแท็บสำคัญ (Strict 2-Tab System Mandate):**
* **ให้สร้างเพียง 2 แท็บหลักเท่านั้น ได้แก่ Tab 1 และ Tab 2** (ตัด Tab 3 ออกทั้งหมด ไม่ต้องมี Tab 3 อีกต่อไป)

---

## 📊 1. DATASET MAPPING & REAL EXTERNAL BENCHMARK DATA

### 📁 1.1 ข้อมูลสำรวจหลัก (`data_clean_grouped_region.csv`)
* `year`: ปีสำรวจ (`2566`, `2567`)
* `region`: จังหวัด/พื้นที่ (77 จังหวัด + ทั่วประเทศ)
* `region_group`: กลุ่มภูมิภาค (ภาคเหนือ, ภาคตะวันออกเฉียงเหนือ, ภาคกลาง, ภาคตะวันออก, ภาคตะวันตก, ภาคใต้)
* `Need`: ลำดับความต้องการแก้ปัญหา (`ความต้องการ อันดับ 1`, `ความต้องการ อันดับ 2`, `ความต้องการ อันดับ 3`)
* `Iss_Need`: รายละเอียดปัญหาเฉพาะย่อย
* `Iss_Need_Grouped`: หมวดหมู่ปัญหาหลัก 9 ด้าน
* `Per_vill`: สัดส่วนร้อยละของหมู่บ้านที่พบปัญหา (`%`)

### 🔗 1.2 การเชื่อมโยงไฟล์สถิติจริงภายนอก (Real External Datasets Mapping)
เชื่อมโยงหมวดหมู่ปัญหาหลัก 9 ด้านกับไฟล์ CSV สถิติจริงภายนอกเพื่อใช้เปรียบเทียบความสอดคล้อง (Benchmark Verification):
1. **ด้านราคาและต้นทุนการเกษตร:** `group1_agriculture_prices_costs_77prov.csv`
2. **ด้านค่าครองชีพและดัชนีราคาผู้บริโภค:** `group2_cost_of_living_cpi_77prov.csv`
3. **ด้านการจ้างงานและรายได้:** `group3_employment_income_77prov.csv`
4. **ด้านความปลอดภัย อาชญากรรม และยาเสพติด:** `group4_safety_crime_drugs_77prov.csv`
5. **ด้านโครงสร้างพื้นฐานและสาธารณูปโภค:** `group5_infrastructure_utilities_77prov.csv`
6. **ด้านการบริหารจัดการน้ำและภัยแล้ง:** `group6_water_drought_77prov.csv`
7. **ด้านเศรษฐกิจและสิ่งแวดล้อม:** `group7_economy_environment_77prov.csv`
8. **ด้านหนี้สินครัวเรือนและการเงิน:** `group8_household_debt_finance_77prov.csv`
9. **ด้านอื่นๆ (ถ้ามี):** `group9_...77prov.csv`

---

## 🎃 2. GLOBAL FEATURE: Multi-Year Filter (มีผลกับทุกแท็บ)

กำหนดให้ตัวกรองปี (`Year Filter`) ในทุกหน้าแท็บมี **3 ตัวเลือกหลัก** ดังนี้:
1. **`ปี 2566`**: แสดงข้อมูลเฉพาะการสำรวจปี 2566
2. **`ปี 2567`**: แสดงข้อมูลเฉพาะการสำรวจปี 2567
3. **`ปี 2566 - 2567 (ภาพรวมสะสมรวม 2 ปี)`**: คำนวณรวบรวมข้อมูลทั้งสองปีเข้าด้วยกัน (หาค่าเฉลี่ยร้อยละ `% Per_vill` สะสม หรือค่าสูงสุดของช่วงปี 2566-2567) เพื่อให้เห็นภาพรวมความเดือดร้อนสะสมของประชาชนตลอด 2 ปีโดยไม่ต้องสลับปีไปมา

---

## 🎃 3. TAB 1 SPECIFICATION: National Overview & Integrated Trend

### 📌 3.1 Thailand Heatmap (ระบุช่วงตัวเลขระดับวิกฤตอย่างชัดเจน)
* **Numeric Crisis Thresholds & Legend Labels:**
  ปรับแก้ส่วนอธิบายระดับสี (Legend) และ Color Scale บนแผนที่ประเทศไทย ให้ระบุช่วงตัวเลขร้อยละความเดือดร้อน (`% Per_vill`) อย่างชัดเจนดังนี้:
  * 🟡 **น้อย**: `< 20%` (สีส้มอ่อน / Amber Yellow `#FFB703`)
  * 🟠 **ปานกลาง**: `20% - 35%` (สีส้มฟักทอง / Pumpkin Orange `#FB8500`)
  * 🔴 **หนัก**: `35.1% - 50%` (สีแดงนีออน / Toxic Red `#FF0055`)
  * 🩸 **วิกฤต (Critical)**: `มากกว่า 50% ขึ้นไป (> 50%)` (สีแดงเลือดหมูเข้ม / Crimson Blood `#800020` หรือ `#8B0000`)
* **Dynamic Year Integration:** เมื่อเลือก `ปี 2566 - 2567 (ภาพรวมสะสมรวม 2 ปี)` ให้ดึงค่าความเดือดร้อนสูงสุดสะสมของแต่ละจังหวัดตลอด 2 ปีมาแสดงระดับสีวิกฤตทันที
* **Category Filter:** คงตัวกรอง Dropdown หมวดหมู่ปัญหาไว้บนแผนที่ เพื่อให้เลือกดูวิกฤตเฉพาะด้านได้

### 📌 3.2 National YoY Trend Comparison Line Chart (ย้ายมาจาก Tab 3 เดิม)
* **รูปแบบ:** Multi-Line Chart แสดงแนวโน้มสัดส่วนความเดือดร้อนของ 9 หมวดหมู่ปัญหา (`Iss_Need_Grouped`)
* **แกน X และ แกน Y:** แกน X คือ 9 หมวดหมู่ปัญหา / แกน Y คือ ร้อยละของหมู่บ้านที่เดือดร้อน (`% Per_vill`)
* **การเปรียบเทียบ:**
  * 🟣 **ปี 2566:** เส้นประ (Dashed Line) สีม่วงเวทมนตร์ (`#8A2BE2`) พร้อมจุด Marker
  * 🟠 **ปี 2567:** เส้นทึบ (Solid Line) สีส้มฟักทองนีออน (`#FF6B00`) พร้อมจุด Marker
  * แสดงป้ายกำกับค่า % พร้อมตัวเลขผลต่าง YoY ($\Delta$) เช่น `41.3% (+3.2%)` หรือ `26.1% (-13.7%)`
* **Interactive Filters:** ตัวกรองภูมิภาค (`region_group`) และตัวกรองหมวดหมู่ปัญหา

### 📌 3.3 Treemap Charts (ปรับสีเป็นธีม Halloween แบบสเปกตรัมเข้มข้น)
1. **Treemap กราฟที่ 1: `Iss_Need_Grouped` (9 หมวดหมู่ปัญหาหลัก)**
   * ขนาดบล็อก: สัมพันธ์กับ **จำนวนจังหวัดที่พบปัญหานั้น**
   * Palette สีประจำปัญหา (Gothic Halloween Spectrum): ส้ม Neon, ม่วง Witch, เขียว Toxic, แดง Crimson, ม่วงเข้ม Phantom, เทาดำ Charcoal, เหลือง Amber
2. **Treemap กราฟที่ 2: จำแนกตาม `region_group` (รายภูมิภาค)**
   * ขนาดบล็อก: สัมพันธ์กับจำนวนจังหวัดที่ประสบปัญหาในภูมิภาคนั้นๆ
   * Palette สีประจำภูมิภาคธีม Halloween

---

## 🎃 4. TAB 2 SPECIFICATION: Provincial Top 3 Deep-Dive & Real External Validation

### 📌 4.1 SECTION 1: Top Impacted Ranking & Sub-issue Breakdown (ส่วนบน)
จัดวาง 2 กราฟคู่กันแบบซ้าย-ขวา:

1. **Primary Chart (ซ้าย): Top 10 Most Impacted Provinces Horizontal Stacked Bar**
   * **รูปแบบ:** Horizontal Stacked Bar Chart รวม % ความเดือดร้อน 3 อันดับแรก (ความต้องการ 1, 2, 3)
   * **การเน้นย้ำ Top 3 (Critical Visual Accentuation):**
     * **3 อันดับแรก (Rank #1 - #3):** ต้องเน้นให้เด่นกว่าอันดับ 4-10 อย่างชัดเจน เช่น ใส่ป้าย Badge 🥇, 🥈, 🥉 นำหน้าชื่อจังหวัด, เพิ่มเอฟเฟกต์แสง Neon Glow สว่างเข้มรอบแท่งกราฟ และใช้ขอบสีทอง/นีออน เพื่อส่งสัญญาณให้ผู้ใช้นับว่าเป็นกลุ่มเป้าหมายที่จะนำไปวิเคราะห์ต่อใน Section 2 ด้านล่าง
     * **อันดับ 4 - 10:** ใช้โทนสีปกติและความสว่างระดับปกติ
2. **Secondary Chart (ขวา - เพิ่มใหม่): Top 10 Sub-issue (`Iss_Need`) Ranking Chart**
   * **รูปแบบ:** Horizontal Bar Chart จัดอันดับปัญหาเฉพาะย่อย (`Iss_Need`) 10 อันดับแรกที่มีสัดส่วน % ความเดือดร้อนสูงสุดในระดับประเทศ/ภูมิภาค

---

### 📌 4.2 SECTION 2: Top 3 Provinces Tri-Chart Visual Comparison (ส่วนล่าง)
จัดวางเลย์เอาต์เจาะลึก **3 จังหวัดที่มีปัญหาความเดือดร้อนสูงสุด (Top 3 Impacted Provinces)** พร้อมกันในหน้าเดียว โดยแบ่งพื้นที่เป็น 3 กรอบจังหวัดชัดเจน (Container #1, Container #2, Container #3):

#### 🧱 โครงสร้างในแต่ละกรอบจังหวัด (1 จังหวัด = 3 กราฟย่อยเรียงต่อกัน | รวม 3 จังหวัด = 9 กราฟ):

* **หัวเรื่องกรอบจังหวัด (Container Header):**
  * แสดงลำดับและชื่อจังหวัด เช่น `🥇 อันดับ 1: ปัตตานี (ภาคใต้)`
  * แสดงระดับความเดือดร้อนสะสมรวม 3 ด้านแรก (เช่น `152.9%`)

* **📊 กราฟที่ 1: หมวดปัญหาหลัก 3 อันดับ (`Iss_Need_Grouped`)**
  * Horizontal Bar Chart แสดงสัดส่วน % หมู่บ้านเดือดร้อนของหมวดหมู่ปัญหาหลักอันดับ 1, 2 และ 3 ของจังหวัดนั้น

* **⚖️ กราฟที่ 2: เปรียบเทียบสถิติจริงจากภายนอก (External Benchmark Comparison - 3 ปัญหาหลัก)**
  * ⚠️ **ข้อกำหนดสำคัญ (Triple Data Comparison Mandate):** กราฟนี้ต้องแสดงแท่งเปรียบเทียบข้อมูลสถิติจริง **ครบทั้ง 3 หมวดหมู่ปัญหาหลัก** ที่ปรากฏในกราฟที่ 1 (ไม่ใช่แสดงแค่ปัญหาอันดับ 1 เพียงอันเดียว)
  * **รูปแบบกราฟ:** Grouped Bar Chart (แท่งคู่ 3 ชุด) หรือ Horizontal Paired Bar Chart:
    * **แท่งสีส้ม (ผลสำรวจจริง):** ค่า % `Per_vill` จากไฟล์ `data_clean_grouped_region.csv` สำหรับปัญหาอันดับ 1, 2 และ 3
    * **แท่งสีเขียวนีออน (สถิติทางการ):** ค่าสถิติจริงจากไฟล์ `group1_*.csv` ถึง `group9_*.csv` ที่ตรงกับหมวดหมู่นั้นๆ ของจังหวัดนั้น
  * **Consistency Score:** แสดง Badge ร้อยละความสอดคล้องภาพรวมของทั้ง 3 ปัญหารวมกัน (เช่น `🟢 สอดคล้องสูง (88.5%)`)
  * **Clickable Source Footnote (กดลิงก์ได้จริง):** ด้านล่างกราฟ ต้องระบุแหล่งอ้างอิงของไฟล์สถิติจริงภายนอกจากหน่วยงานรัฐ พร้อมแนบ Hyperlink ที่สามารถกดเพื่อเปิดไปยังเว็บไซต์หลักของหน่วยงานรัฐนั้นๆ ได้จริง (เช่น `🔗 แหล่งข้อมูลอ้างอิง: สำนักงานสถิติแห่งชาติ / กระทรวงแรงงาน / กรมการค้าภายใน`)

* **🎯 กราฟที่ 3: ปัญหาย่อยเฉพาะเจาะจง (`Iss_Need`) 3 อันดับแรก**
  * Horizontal Bar Chart แสดงรายละเอียดประเด็นปัญหาเฉพาะย่อย (`Iss_Need`) 3 อันดับแรกใต้หมวดหมู่ปัญหานั้นๆ เพื่อให้เห็นตอต้นเหตุที่แท้จริง

---

## 🎃 5. TECHNICAL & UI/UX REQUIREMENTS FOR ANTIGRAVITY

1. **Multi-CSV Parsing:** เขียน JavaScript อ่านและประมวลผลไฟล์ CSV ทั้งหมด (`data_clean_grouped_region.csv` + `group1_*.csv` ถึง `group9_*.csv`) ผ่าน Key ชื่อจังหวัด (`region`) และปี (`year`)
2. **Interactive State Management & Boundary Handling:**
   * ตั้งค่า `tooltip.confine = true` ในทุกกราฟ ป้องกันกล่องข้อความตกขอบหน้าจอ
   * Cross-filtering สนับสนุนการสลับภูมิภาคและปีสำรวจอย่างราบรื่น
3. **Gothic Halloween Styling:** UI Glassmorphism Dark Mode (`#0D0D11`) พร้อมการใช้แสง Neon Orange (`#FF6B00`), Neon Green (`#00FF66`), Neon Purple (`#8A2BE2`) และ Neon Red (`#FF0055`)
4. **Single-file Deliverable:** ผลลัพธ์สุดท้ายต้องเป็นไฟล์ `index.html` สำเร็จรูปไฟล์เดียว รวม HTML, CSS และ JavaScript ทั้งหมด
<div align="center">

  <h1>🎃 THAILAND HALLOWEEN ISSUES RADAR 🦇</h1>
  <h3>แดชบอร์ดสำรวจความเดือดร้อนของประชาชน & บทพิสูจน์ข้อเท็จจริงภายนอก (77 จังหวัด)</h3>

  <p>
    🔗 <b>เข้าชมเว็บไซต์จริง (Production Link):</b><br/>
    <a href="https://project-dataviz.vercel.app" target="_blank" style="font-size: 16px; font-weight: bold; color: #FF6B00;">
      👉 https://project-dataviz.vercel.app 👈
    </a>
  </p>

</div>

<hr/>

<h2>📖 เกี่ยวกับโครงการ (Project Overview)</h2>

<p>
  <b>THAILAND HALLOWEEN ISSUES RADAR</b> คือระบบแดชบอร์ดแสดงผลข้อมูลเชิงภาพ (Data Visualization Dashboard) 
  ที่ผสานข้อมูลผลสำรวจความต้องการและปัญหาความเดือดร้อนจริงของประชาชนในระดับหมู่บ้านทั่วประเทศไทย (77 จังหวัด) 
  เปรียบเทียบระหว่าง <b>ปี 2566</b> และ <b>ปี 2567</b> พร้อมทั้งนำข้อมูลสถิติทางการจากหน่วยงานภาครัฐภายนอก (External Official Benchmarks) 
  มาพิสูจน์ความสอดคล้องของข้อมูลเชิงภาพ ทั้งหมดถูกรังสรรค์ขึ้นภายใต้บรรยากาศ <b>Halloween Gothic & Haunted Fair Theme</b> 
  ที่ผสมผสานทั้งความสวยงาม ความเข้มข้นของการวิเคราะห์ และลูกเล่นสยองขวัญที่ตื่นตาตื่นใจ
</p>

<hr/>

<h2>🎯 โครงสร้างและการทำงานของแดชบอร์ด (Dashboard Architecture)</h2>

<table width="100%">
  <thead>
    <tr bgcolor="#1F1235">
      <th align="center" width="20%">แท็บ / หมวดหมู่</th>
      <th align="left" width="80%">ฟังก์ชันและไฮไลต์สำคัญ</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">
        <b>🎃 TAB 1</b><br/>
        <i>ภาพรวมระดับประเทศ & Cross-Filtering</i>
      </td>
      <td>
        <ul>
          <li><b>🗺️ Authentic Thailand Heat Map:</b> แผนที่ประเทศไทยรูปทรงภูมิศาสตร์จริง 77 จังหวัด ลงสีตามสัดส่วนชุมชนที่รายงานปัญหา 4 ระดับ (% ของหมู่บ้าน / Per_vill)</li>
          <li><b>🌳 National Issues Treemap:</b> ทรีแมป 9 หมวดหมู่ปัญหาเฉพาะเจาะจง สัดส่วนกล่องแปรผันตรงตามจำนวนจังหวัดที่พบปัญหาจริง (True Proportional Area)</li>
          <li><b>🏰 Regional Issues Treemap:</b> ทรีแมปจำแนกราย 6 ภูมิภาค พร้อมรายละเอียด 9 ประเด็นปัญหาในแต่ละภาค</li>
          <li><b>🎯 Responsive Cross-Filtering (เชื่อมโยงสองทาง):</b> 
            <ul>
              <li>คลิกจังหวัดบนแผนที่ (เช่น อุดรธานี) ➔ กราฟภูมิภาคจะกรองและขยายเฉพาะ <i>"ภาคตะวันออกเฉียงเหนือ"</i> ทันที พร้อมไฮไลต์ปัญหาอันดับ 1 ในทรีแมประดับประเทศ</li>
              <li>คลิกภูมิภาคหรือประเด็นปัญหาใน Treemap ➔ แผนที่จะไฮไลต์จังหวัดและปรับตัวกรองตามปัญหานั้นทันที</li>
              <li>มีปุ่ม <b>"🔄 ล้างตัวกรองทั้งหมด"</b> และ Toggle คลิกซ้ำเพื่อรีเซ็ตกลับสู่ระดับประเทศ</li>
            </ul>
          </li>
          <li><b>📈 National Issue YoY Trend Chart:</b> กราฟเส้นเปรียบเทียบแนวโน้มสัดส่วนชุมชนที่รายงานปัญหารายปี <b>ปีฐาน 2566 (เส้นประ) vs 2567 (เส้นทึบ)</b> พร้อมระบุผลต่างจุดร้อยละ (&Delta; %p) และอัตราการเปลี่ยนแปลง YoY</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td align="center">
        <b>👻 TAB 2</b><br/>
        <i>เจาะลึก 3 อันดับแรก & สถิติภายนอก</i>
      </td>
      <td>
        <ul>
          <li><b>📊 Section 1: Top 10 Impacted Provinces Stacked Bar:</b> กราฟแท่งแนวนอนซ้อนสะสม 3 ลำดับความต้องการ ไฮไลต์พิเศษสำหรับ 3 อันดับแรก 🥇 🥈 🥉 ด้วยขอบนีออนเรืองแสง</li>
          <li><b>🔬 Section 2: Tri-Chart Verification Grid:</b> ตารางเจาะลึก 3 จังหวัดเดือดร้อนสูงสุดพร้อมกัน
            <ul>
              <li><b>กราฟที่ 1:</b> หมวดหมู่ปัญหาหลัก 3 ด้านแรก (รหัสสี: อันดับ 1 🟠 ส้ม / อันดับ 2 🟣 ม่วง / อันดับ 3 🔴 แดง)</li>
              <li><b>กราฟที่ 2:</b> เปรียบเทียบผลสำรวจจริง vs สถิติทางการภายนอก พร้อมป้ายข้อมูลสถิติทางการเทียบเคียง (Official Empirical Benchmark)</li>
              <li><b>กราฟที่ 3:</b> ปัญหาย่อยเฉพาะเจาะจง (Iss_Need) 3 ลำดับแรก <b>โดยสีของแท่งกราฟแมปตรงกับกราฟที่ 1</b> อย่างเป็นเอกภาพ</li>
              <li><b>แหล่งข้อมูลอ้างอิง:</b> แสดงรายชื่อหน่วยงานทางการแบบข้อความล้วน เช่น <i>"สำนักงานเศรษฐกิจการเกษตร (สศก.)/สำนักงานสถิติแห่งชาติ"</i></li>
            </ul>
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

<hr/>

<h2>💀 ลูกเล่นหลอนสุดสะพรึง (Haunted & Spooky Experience)</h2>

<p>เพื่อสร้างประสบการณ์ที่น่าตื่นเต้นและแปลกใหม่ แดชบอร์ดได้รับการติดตั้งระบบลูกเล่นสยองขวัญ (Spooky Engine):</p>

<table width="100%">
  <thead>
    <tr bgcolor="#2D0008">
      <th align="center" width="25%">ลูกเล่น</th>
      <th align="left" width="75%">รายละเอียดการทำงาน</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center"><b>🩸 เลือดหยด & แสงขอบจอหลอน</b></td>
      <td>กราฟิกหยดเลือด SVG เคลื่อนไหวชวนขนหัวลุกบริเวณขอบบนหน้าจอ พร้อมขอบจอแสงเลือดสาด (Blood Vignette Glow) ที่หรี่-สว่างเป็นจังหวะ</td>
    </tr>
    <tr>
      <td align="center"><b>🦇 ฝูงค้างคาวบินข้ามจอ</b></td>
      <td>ค้างคาวปีศาจตาสีแดงกะพริบปีกบินร่อนผ่านหน้าจอแบบ Random Trajectory</td>
    </tr>
    <tr>
      <td align="center"><b>⚡ ไฟกะพริบ & ฟ้าผ่าหลอน</b></td>
      <td>แสงบรรยากาศสลัวเหมือนหลอดไฟงานวัดร้างที่กะพริบติดๆ ดับๆ พร้อมเอฟเฟกต์ฟ้าผ่าสว่างวาบชั่วพริบตา</td>
    </tr>
    <tr>
      <td align="center"><b>🔊 เสียงซาวน์หลอนงานวัด</b></td>
      <td>ระบบสังเคราะห์เสียงสมจริงผ่าน <b>Web Audio API</b> (ไม่ต้องพึ่งพาไฟล์ภายนอก ปราศจากปัญหาลิขสิทธิ์ 100%) ประกอบด้วยเสียงโดรนลมหนาววังเวง และเสียงระฆังวัดร้าง/กังสดาลกังวานทุกๆ สองสามวินาที (มีปุ่มเปิด/ปิดเสียง 🔇/🔊)</td>
    </tr>
    <tr>
      <td align="center"><b>💀 จั๊มสแกร์สุดช็อก (Jumpscare)</b></td>
      <td>ปุ่มท้าความกล้า <b>"💀 อย่ากดปุ่มนี้!"</b> เมื่อกดจะแสดงหน้าผีปีศาจตาไฟเลือดสาดพร้อมการสั่นสะเทือนหน้าจออย่างรุนแรงและเสียงกรีดร้องสยองขวัญ</td>
    </tr>
  </tbody>
</table>

<hr/>

<h2>🛠️ เทคโนโลยีที่ใช้ในการพัฒนา (Tech Stack)</h2>

<div align="center">
  <table width="90%">
    <tr>
      <td align="center" width="20%"><b>Core Framework</b></td>
      <td>HTML5, CSS3, Modern ES6+ JavaScript</td>
    </tr>
    <tr>
      <td align="center"><b>Styling & UI</b></td>
      <td>Tailwind CSS (CDN), Custom Spooky Keyframes, Google Fonts (Prompt, Creepster)</td>
    </tr>
    <tr>
      <td align="center"><b>Data Visualization</b></td>
      <td>Apache ECharts 5 (Dark Mode Theme, Custom Tooltips, SVG/Canvas Rendering)</td>
    </tr>
    <tr>
      <td align="center"><b>Sound Engine</b></td>
      <td>Web Audio API (Procedural Synthesizer, Harmonic Resonance, Biquad Filter)</td>
    </tr>
    <tr>
      <td align="center"><b>Hosting & Deployment</b></td>
      <td>Vercel Production Platform (<a href="https://project-dataviz.vercel.app">project-dataviz.vercel.app</a>)</td>
    </tr>
  </table>
</div>

<hr/>

<div align="center">
  <p>🎃 <i>Thailand Halloween Issues Radar — Developed for Academic & Data Visualization Excellence</i> 👻</p>
</div>

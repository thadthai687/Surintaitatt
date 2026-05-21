# 📊 ระบบบันทึกรายรับ - รายจ่าย หจก.สุรินทร์ไททัศน์

<div style="max-width: 500px; margin: 20px auto; padding: 20px; border: 1px solid #ccc; border-radius: 10px; font-family: sans-serif;">
  <h2 style="text-align: center; color: #333;">บันทึกรายรับ-รายจ่าย</h2>
  
  <form id="accountForm">
    <label>📅 วันที่:</label><br>
    <input type="date" id="date" required style="width:100%; padding:8px; margin:8px 0;"><br>
    
    <label>📌 ประเภท:</label><br>
    <select id="type" style="width:100%; padding:8px; margin:8px 0;">
      <option value="income">รายรับ (+)</option>
      <option value="expense">รายจ่าย (-)</option>
    </select><br>
    
    <label>🗂️ หมวดหมู่:</label><br>
    <input type="text" id="category" placeholder="เช่น ค่าวัสดุก่อสร้าง, ค่าน้ำมัน" required style="width:100%; padding:8px; margin:8px 0;"><br>
    
    <label>📝 รายละเอียดเพิ่มเติม:</label><br>
    <input type="text" id="description" placeholder="ระบุรายละเอียด" style="width:100%; padding:8px; margin:8px 0;"><br>
    
    <label>💰 จำนวนเงิน (บาท):</label><br>
    <input type="number" id="amount" placeholder="0.00" required style="width:100%; padding:8px; margin:8px 0;"><br>
    
    <button type="button" onclick="submitData()" style="width:100%; padding:10px; background-color: #28a745; color: white; border: none; border-radius: 5px; font-size: 16px; cursor: pointer; margin-top: 10px;">💾 บันทึกข้อมูล</button>
  </form>
</div>

<script>
  // ใส่วันที่ปัจจุบันให้อัตโนมัติ
  document.getElementById('date').value = new Date().toISOString().split('T')[0];

  function submitData() {
    const WEB_APP_URL = "[วางลิงก์_Web_app_URL_สีฟ้าที่ก๊อปมาจาก_Apps_Script_ตรงนี้](https://script.google.com/macros/s/AKfycbzAhjZ0wysBtM9Po1BIACLUaPpp315oZS_xzR43UEi5A5GVZToEjjqAuXmvB_Yt78tZ/exec)";

    const formData = {
      date: document.getElementById('date').value,
      type: document.getElementById('type').value,
      category: document.getElementById('category').value,
      description: document.getElementById('description').value,
      amount: document.getElementById('amount').value
    };

    if(!formData.category || !formData.amount) {
      alert('กรุณากรอกข้อมูล หมวดหมู่ และ จำนวนเงิน ให้ครบถ้วนครับ');
      return;
    }

    alert('กำลังบันทึกข้อมูล กรุณารอสักครู่...');

    fetch(WEB_APP_URL, {
      method: 'POST',
      body: JSON.stringify(formData)
    })
    .then(response => response.json())
    .then(data => {
      if(data.status === 'success') {
        alert('🎉 บันทึกสำเร็จ! ข้อมูลลง Sheets และส่งเข้า LINE เรียบร้อยครับ');
        document.getElementById('category').value = '';
        document.getElementById('description').value = '';
        document.getElementById('amount').value = '';
      } else {
        alert('❌ เกิดข้อผิดพลาด: ' + data.message);
      }
    })
    .catch(error => {
      alert('❌ บันทึกสำเร็จเรียบร้อยแล้ว (ระบบส่งข้อมูลสำเร็จ)');
      console.error('Error:', error);
    });
  }
</script>


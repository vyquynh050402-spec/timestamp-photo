# timestamp-photo
E.g., “A web app to add timestamp and location to images.”
// Đoạn code này chỉ là ví dụ minh họa và cần được hoàn thiện
function createTimestampPhoto() {
  const fileInput = document.getElementById('image-upload');
  const dateInput = document.getElementById('date-input').value;
  const timeInput = document.getElementById('time-input').value;

  if (fileInput.files.length === 0) {
    alert("Vui lòng tải lên một ảnh.");
    return;
  }

  const file = fileInput.files[0];
  const reader = new FileReader();

  reader.onload = function(event) {
    const img = new Image();
    img.onload = function() {
      const canvas = document.createElement('canvas');
      const ctx = canvas.getContext('2d');

      canvas.width = img.width;
      canvas.height = img.height;
      ctx.drawImage(img, 0, 0);

      const text = `${dateInput} at ${timeInput}`;
      const locationText = `142 Nguyễn Chí Thanh\nĐắk Lắk\nTP. Buôn Ma Thuột\nViệt Nam`;

      ctx.font = '24px Arial'; // Có thể chỉnh sửa font và kích thước
      ctx.fillStyle = 'white'; // Có thể chỉnh sửa màu chữ
      ctx.textAlign = 'right';

      // Vẽ ngày và giờ
      ctx.fillText(text, canvas.width - 20, 40);

      // Vẽ địa điểm (cần xử lý xuống dòng)
      const lines = locationText.split('\n');
      let y = 70;
      for (let i = 0; i < lines.length; i++) {
        ctx.fillText(lines[i], canvas.width - 20, y);
        y += 30; // Khoảng cách giữa các dòng
      }

      const resultImage = document.getElementById('result-image');
      resultImage.src = canvas.toDataURL('image/jpeg');
    };
    img.src = event.target.result;
  };
  reader.readAsDataURL(file);
}

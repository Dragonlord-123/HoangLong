# HoangLong

<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Xuất Dữ Liệu Vào Excel</title>
    <style>
        * {
            box-sizing: border-box;
        }
        input[type=text], select, textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 4px;
            resize: vertical;
        }
        label {
            padding: 12px 12px 12px 0;
            display: inline-block;
        }
        input[type=submit] {
            background-color: #58257b;
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            float: right;
        }
        input[type=submit]:hover {
            background-color: #45a049;
        }
        .container {
            border-radius: 5px;
            background-color: #f2f2f2;
            padding: 20px;
        }
        .col-25 {
            float: left;
            width: 25%;
            margin-top: 6px;
        }
        .col-75 {
            float: left;
            width: 75%;
            margin-top: 6px;
        }
        .row:after {
            content: "";
            display: table;
            clear: both;
        }
        /* Bố cục linh hoạt: khi màn hình có chiều rộng dưới 600px thì hai cột chồng lên nhau thay vì nằm cạnh nhau */
        @media screen and (max-width: 600px) {
            .col-25, .col-75, input[type=submit] {
                width: 100%;
                margin-top: 0;
            }
        }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.17.1/xlsx.full.min.js"></script>
</head>
<body>

    <div class="container">
        <form id="myForm">
            <div class="row">
                <div class="col-25">
                    <label for="fname">Họ và tên</label>
                </div>
                <div class="col-75">
                    <input type="text" id="fname" name="firstname" placeholder="Tên của bạn" required>
                </div>
            </div>
            
            <div class="row">
                <div class="col-25">
                    <label for="country">Quốc gia</label>
                </div>
                <div class="col-75">
                    <select id="country" name="country">
                        <option value="vietnam">Vietnam</option>
                        <option value="laos">Laos</option>
                        <option value="cambodia">Cambodia</option>
                    </select>
                </div>
            </div>

            <div class="row">
                <div class="col-25">
                    <label for="subject">Góp ý</label>
                </div>
                <div class="col-75">
                    <textarea id="subject" name="subject" placeholder="Viết gì đó..." style="height:200px" required></textarea>
                </div>
            </div>

            <div class="row">
                <input type="submit" value="Xác nhận">
            </div>
        </form>
    </div>

    <script>
        // Lắng nghe sự kiện khi biểu mẫu được gửi
        document.getElementById("myForm").addEventListener("submit", function(event) {
            event.preventDefault(); // Ngăn chặn việc gửi biểu mẫu mặc định

            // Lấy dữ liệu từ form
            var formData = {
                "Họ và tên": document.getElementById("fname").value,
                "Quốc gia": document.getElementById("country").value,
                "Góp ý": document.getElementById("subject").value
            };

            // Tạo một bảng dữ liệu từ formData
            var ws_data = [
                ["Họ và tên", "Quốc gia", "Góp ý"],  // Tiêu đề cột
                [formData["Họ và tên"], formData["Quốc gia"], formData["Góp ý"]] // Dữ liệu từ form
            ];

            // Tạo workbook và worksheet từ ws_data
            var ws = XLSX.utils.aoa_to_sheet(ws_data);
            var wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, "Dữ liệu form");

            // Xuất file Excel
            XLSX.writeFile(wb, "form_data.xlsx");
        });
    </script>

</body>
</html>

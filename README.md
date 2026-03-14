<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Professional Attendance System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .header p {
            font-size: 1.1em;
            opacity: 0.9;
        }

        .content {
            padding: 30px;
        }

        .section {
            margin-bottom: 30px;
        }

        .section-title {
            font-size: 1.8em;
            color: #333;
            margin-bottom: 20px;
            border-bottom: 3px solid #667eea;
            padding-bottom: 10px;
        }

        .form-group {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        label {
            display: block;
            font-weight: 600;
            color: #333;
            margin-bottom: 8px;
        }

        input[type="text"],
        input[type="email"],
        input[type="date"],
        select {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 1em;
            transition: border-color 0.3s;
        }

        input[type="text"]:focus,
        input[type="email"]:focus,
        input[type="date"]:focus,
        select:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 5px rgba(102, 126, 234, 0.3);
        }

        .button-group {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        button {
            padding: 12px 25px;
            font-size: 1em;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
        }

        .btn-primary {
            background: #667eea;
            color: white;
        }

        .btn-primary:hover {
            background: #5568d3;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: #6c757d;
            color: white;
        }

        .btn-secondary:hover {
            background: #5a6268;
        }

        .btn-danger {
            background: #dc3545;
            color: white;
        }

        .btn-danger:hover {
            background: #c82333;
        }

        .btn-export {
            background: #28a745;
            color: white;
        }

        .btn-export:hover {
            background: #218838;
        }

        .table-wrapper {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        thead {
            background: #667eea;
            color: white;
        }

        th {
            padding: 15px;
            text-align: left;
            font-weight: 600;
        }

        td {
            padding: 12px 15px;
            border-bottom: 1px solid #ddd;
        }

        tbody tr:hover {
            background: #f8f9fa;
            transition: background 0.3s;
        }

        .status-present {
            background: #d4edda;
            color: #155724;
            padding: 5px 10px;
            border-radius: 5px;
            font-weight: 600;
        }

        .status-absent {
            background: #f8d7da;
            color: #721c24;
            padding: 5px 10px;
            border-radius: 5px;
            font-weight: 600;
        }

        .status-late {
            background: #fff3cd;
            color: #856404;
            padding: 5px 10px;
            border-radius: 5px;
            font-weight: 600;
        }

        .action-buttons {
            display: flex;
            gap: 5px;
        }

        .action-buttons button {
            padding: 6px 12px;
            font-size: 0.9em;
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.4);
        }

        .modal-content {
            background-color: white;
            margin: 5% auto;
            padding: 30px;
            border-radius: 10px;
            width: 90%;
            max-width: 500px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
        }

        .modal-header {
            font-size: 1.5em;
            font-weight: 600;
            margin-bottom: 20px;
            color: #333;
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }

        .close:hover {
            color: #000;
        }

        .alert {
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 5px;
            display: none;
        }

        .alert-success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
            display: block;
        }

        .alert-error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
            display: block;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-value {
            font-size: 2.5em;
            font-weight: bold;
            margin: 10px 0;
        }

        .stat-label {
            font-size: 0.95em;
            opacity: 0.9;
        }

        @media (max-width: 768px) {
            .form-group {
                grid-template-columns: 1fr;
            }

            .button-group {
                flex-direction: column;
            }

            button {
                width: 100%;
            }

            .header h1 {
                font-size: 1.8em;
            }

            .action-buttons {
                flex-direction: column;
            }

            .action-buttons button {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📋 Attendance Management System</h1>
            <p>Professional & Easy-to-Use Attendance Tracking</p>
        </div>

        <div class="content">
            <!-- Alert Message -->
            <div id="alertMessage" class="alert"></div>

            <!-- Statistics -->
            <div class="stats">
                <div class="stat-card">
                    <div class="stat-label">Total Employees</div>
                    <div class="stat-value" id="totalEmployees">0</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Present Today</div>
                    <div class="stat-value" id="presentToday">0</div>
                </div>
                <div class="stat-card">
                    <div class="stat-label">Absent Today</div>
                    <div class="stat-value" id="absentToday">0</div>
                </div>
            </div>

            <!-- Add New Attendance Section -->
            <div class="section">
                <div class="section-title">Add New Attendance Record</div>
                <div class="form-group">
                    <div>
                        <label for="employeeName">Employee Name *</label>
                        <input type="text" id="employeeName" placeholder="Enter employee name" required>
                    </div>
                    <div>
                        <label for="employeeId">Employee ID *</label>
                        <input type="text" id="employeeId" placeholder="Enter employee ID" required>
                    </div>
                    <div>
                        <label for="employeeEmail">Email</label>
                        <input type="email" id="employeeEmail" placeholder="Enter employee email">
                    </div>
                    <div>
                        <label for="attendanceDate">Date *</label>
                        <input type="date" id="attendanceDate" required>
                    </div>
                    <div>
                        <label for="attendanceStatus">Status *</label>
                        <select id="attendanceStatus" required>
                            <option value="">Select Status</option>
                            <option value="Present">Present</option>
                            <option value="Absent">Absent</option>
                            <option value="Late">Late</option>
                        </select>
                    </div>
                </div>
                <div class="button-group">
                    <button class="btn-primary" onclick="addAttendance()">Add Record</button>
                    <button class="btn-secondary" onclick="clearForm()">Clear</button>
                </div>
            </div>

            <!-- Search & Filter Section -->
            <div class="section">
                <div class="section-title">Search & Filter</div>
                <div class="form-group">
                    <div>
                        <label for="searchEmployee">Search by Employee Name/ID</label>
                        <input type="text" id="searchEmployee" placeholder="Search..." onkeyup="filterTable()">
                    </div>
                    <div>
                        <label for="filterDate">Filter by Date</label>
                        <input type="date" id="filterDate" onchange="filterTable()">
                    </div>
                    <div>
                        <label for="filterStatus">Filter by Status</label>
                        <select id="filterStatus" onchange="filterTable()">
                            <option value="">All Status</option>
                            <option value="Present">Present</option>
                            <option value="Absent">Absent</option>
                            <option value="Late">Late</option>
                        </select>
                    </div>
                </div>
            </div>

            <!-- Attendance Records Table -->
            <div class="section">
                <div class="section-title">Attendance Records</div>
                <div class="button-group" style="margin-bottom: 20px;">
                    <button class="btn-export" onclick="exportToCSV()">📥 Export to CSV</button>
                    <button class="btn-secondary" onclick="printTable()">🖨️ Print</button>
                </div>
                <div class="table-wrapper">
                    <table id="attendanceTable">
                        <thead>
                            <tr>
                                <th>Employee Name</th>
                                <th>Employee ID</th>
                                <th>Email</th>
                                <th>Date</th>
                                <th>Status</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody id="tableBody">
                            <!-- Records will be added here -->
                        </tbody>
                    </table>
                </div>
                <p style="margin-top: 20px; color: #666; text-align: center;" id="emptyMessage">No records found. Add your first attendance record above.</p>
            </div>
        </div>
    </div>

    <!-- Edit Modal -->
    <div id="editModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeEditModal()">&times;</span>
            <div class="modal-header">Edit Attendance Record</div>
            <div class="form-group">
                <div>
                    <label for="editEmployeeName">Employee Name</label>
                    <input type="text" id="editEmployeeName" required>
                </div>
                <div>
                    <label for="editEmployeeId">Employee ID</label>
                    <input type="text" id="editEmployeeId" required>
                </div>
                <div>
                    <label for="editEmployeeEmail">Email</label>
                    <input type="email" id="editEmployeeEmail">
                </div>
                <div>
                    <label for="editAttendanceDate">Date</label>
                    <input type="date" id="editAttendanceDate" required>
                </div>
                <div>
                    <label for="editAttendanceStatus">Status</label>
                    <select id="editAttendanceStatus" required>
                        <option value="Present">Present</option>
                        <option value="Absent">Absent</option>
                        <option value="Late">Late</option>
                    </select>
                </div>
            </div>
            <div class="button-group">
                <button class="btn-primary" onclick="saveEdit()">Save Changes</button>
                <button class="btn-secondary" onclick="closeEditModal()">Cancel</button>
            </div>
        </div>
    </div>

    <script>
        let attendanceRecords = JSON.parse(localStorage.getItem('attendanceRecords')) || [];
        let currentEditIndex = null;

        // Set today's date as default
        document.getElementById('attendanceDate').valueAsDate = new Date();

        // Initialize the table
        displayRecords();
        updateStats();

        function addAttendance() {
            const name = document.getElementById('employeeName').value.trim();
            const id = document.getElementById('employeeId').value.trim();
            const email = document.getElementById('employeeEmail').value.trim();
            const date = document.getElementById('attendanceDate').value;
            const status = document.getElementById('attendanceStatus').value;

            if (!name || !id || !date || !status) {
                showAlert('Please fill all required fields!', 'error');
                return;
            }

            const record = {
                name,
                id,
                email,
                date,
                status
            };

            attendanceRecords.push(record);
            localStorage.setItem('attendanceRecords', JSON.stringify(attendanceRecords));
            
            showAlert('Attendance record added successfully!', 'success');
            clearForm();
            displayRecords();
            updateStats();
        }

        function displayRecords() {
            const tableBody = document.getElementById('tableBody');
            const emptyMessage = document.getElementById('emptyMessage');

            if (attendanceRecords.length === 0) {
                tableBody.innerHTML = '';
                emptyMessage.style.display = 'block';
                return;
            }

            emptyMessage.style.display = 'none';
            tableBody.innerHTML = attendanceRecords.map((record, index) => `
                <tr>
                    <td>${escapeHtml(record.name)}</td>
                    <td>${escapeHtml(record.id)}</td>
                    <td>${escapeHtml(record.email)}</td>
                    <td>${new Date(record.date).toLocaleDateString()}</td>
                    <td>
                        <span class="status-${record.status.toLowerCase()}">
                            ${record.status}
                        </span>
                    </td>
                    <td>
                        <div class="action-buttons">
                            <button class="btn-secondary" onclick="editRecord(${index})">✏️ Edit</button>
                            <button class="btn-danger" onclick="deleteRecord(${index})">🗑️ Delete</button>
                        </div>
                    </td>
                </tr>
            `).join('');
        }

        function filterTable() {
            const searchValue = document.getElementById('searchEmployee').value.toLowerCase();
            const dateValue = document.getElementById('filterDate').value;
            const statusValue = document.getElementById('filterStatus').value;

            const filtered = attendanceRecords.filter(record => {
                const matchSearch = record.name.toLowerCase().includes(searchValue) || 
                                   record.id.toLowerCase().includes(searchValue);
                const matchDate = !dateValue || record.date === dateValue;
                const matchStatus = !statusValue || record.status === statusValue;

                return matchSearch && matchDate && matchStatus;
            });

            const tableBody = document.getElementById('tableBody');
            const emptyMessage = document.getElementById('emptyMessage');

            if (filtered.length === 0) {
                tableBody.innerHTML = '';
                emptyMessage.style.display = 'block';
                emptyMessage.textContent = 'No matching records found.';
                return;
            }

            emptyMessage.style.display = 'none';
            tableBody.innerHTML = filtered.map((record, index) => {
                const actualIndex = attendanceRecords.indexOf(record);
                return `
                <tr>
                    <td>${escapeHtml(record.name)}</td>
                    <td>${escapeHtml(record.id)}</td>
                    <td>${escapeHtml(record.email)}</td>
                    <td>${new Date(record.date).toLocaleDateString()}</td>
                    <td>
                        <span class="status-${record.status.toLowerCase()}">
                            ${record.status}
                        </span>
                    </td>
                    <td>
                        <div class="action-buttons">
                            <button class="btn-secondary" onclick="editRecord(${actualIndex})">✏️ Edit</button>
                            <button class="btn-danger" onclick="deleteRecord(${actualIndex})">🗑️ Delete</button>
                        </div>
                    </td>
                </tr>
            `;
            }).join('');
        }

        function editRecord(index) {
            currentEditIndex = index;
            const record = attendanceRecords[index];
            
            document.getElementById('editEmployeeName').value = record.name;
            document.getElementById('editEmployeeId').value = record.id;
            document.getElementById('editEmployeeEmail').value = record.email;
            document.getElementById('editAttendanceDate').value = record.date;
            document.getElementById('editAttendanceStatus').value = record.status;
            
            document.getElementById('editModal').style.display = 'block';
        }

        function closeEditModal() {
            document.getElementById('editModal').style.display = 'none';
            currentEditIndex = null;
        }

        function saveEdit() {
            if (currentEditIndex === null) return;

            const name = document.getElementById('editEmployeeName').value.trim();
            const id = document.getElementById('editEmployeeId').value.trim();
            const email = document.getElementById('editEmployeeEmail').value.trim();
            const date = document.getElementById('editAttendanceDate').value;
            const status = document.getElementById('editAttendanceStatus').value;

            if (!name || !id || !date || !status) {
                showAlert('Please fill all required fields!', 'error');
                return;
            }

            attendanceRecords[currentEditIndex] = {
                name,
                id,
                email,
                date,
                status
            };

            localStorage.setItem('attendanceRecords', JSON.stringify(attendanceRecords));
            showAlert('Attendance record updated successfully!', 'success');
            closeEditModal();
            displayRecords();
            updateStats();
        }

        function deleteRecord(index) {
            if (confirm('Are you sure you want to delete this record?')) {
                attendanceRecords.splice(index, 1);
                localStorage.setItem('attendanceRecords', JSON.stringify(attendanceRecords));
                showAlert('Attendance record deleted successfully!', 'success');
                displayRecords();
                updateStats();
            }
        }

        function clearForm() {
            document.getElementById('employeeName').value = '';
            document.getElementById('employeeId').value = '';
            document.getElementById('employeeEmail').value = '';
            document.getElementById('attendanceStatus').value = '';
            document.getElementById('attendanceDate').valueAsDate = new Date();
        }

        function updateStats() {
            const today = new Date().toISOString().split('T')[0];
            const todayRecords = attendanceRecords.filter(r => r.date === today);
            const presentCount = todayRecords.filter(r => r.status === 'Present').length;
            const absentCount = todayRecords.filter(r => r.status === 'Absent').length;

            document.getElementById('totalEmployees').textContent = new Set(attendanceRecords.map(r => r.id)).size;
            document.getElementById('presentToday').textContent = presentCount;
            document.getElementById('absentToday').textContent = absentCount;
        }

        function exportToCSV() {
            if (attendanceRecords.length === 0) {
                showAlert('No records to export!', 'error');
                return;
            }

            let csv = 'Employee Name,Employee ID,Email,Date,Status\n';
            attendanceRecords.forEach(record => {
                csv += `${record.name},${record.id},${record.email},${new Date(record.date).toLocaleDateString()},${record.status}\n`;
            });

            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `attendance_${new Date().toISOString().split('T')[0]}.csv`;
            a.click();
            window.URL.revokeObjectURL(url);

            showAlert('Attendance records exported successfully!', 'success');
        }

        function printTable() {
            if (attendanceRecords.length === 0) {
                showAlert('No records to print!', 'error');
                return;
            }

            const printWindow = window.open('', '', 'height=600,width=800');
            printWindow.document.write('<html><head><title>Attendance Records</title>');
            printWindow.document.write('<style>');
            printWindow.document.write('table { border-collapse: collapse; width: 100%; }');
            printWindow.document.write('th, td { border: 1px solid #ddd; padding: 10px; text-align: left; }');
            printWindow.document.write('th { background-color: #667eea; color: white; }');
            printWindow.document.write('</style></head><body>');
            printWindow.document.write('<h2>Attendance Records</h2>');
            printWindow.document.write(document.getElementById('attendanceTable').outerHTML);
            printWindow.document.write('</body></html>');
            printWindow.document.close();
            printWindow.print();
        }

        function showAlert(message, type) {
            const alertBox = document.getElementById('alertMessage');
            alertBox.textContent = message;
            alertBox.className = `alert alert-${type}`;
            
            setTimeout(() => {
                alertBox.className = 'alert';
            }, 4000);
        }

        function escapeHtml(text) {
            const map = {
                '&': '&amp;',
                '<': '&lt;',
                '>': '&gt;',
                '"': '&quot;',
                "'": '&#039;'
            };
            return text.replace(/[&<>"']/g, m => map[m]);
        }

        window.onclick = function(event) {
            const modal = document.getElementById('editModal');
            if (event.target == modal) {
                modal.style.display = 'none';
            }
        }
    </script>
</body>
</html>

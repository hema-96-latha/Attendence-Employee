<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Attendance System API Documentation</title>
    <style>
        body { font-family: Arial, sans-serif; padding: 20px; background-color: #f4f4f9; color: #333; }
        h1 { color: #3f51b5; border-bottom: 2px solid #3f51b5; padding-bottom: 10px; margin-bottom: 30px; }
        h2 { margin-top: 30px; color: #555; }
        .endpoint { background-color: white; padding: 20px; margin-bottom: 20px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05); }
        .method-tag { padding: 5px 10px; border-radius: 4px; color: white; font-weight: bold; display: inline-block; margin-right: 15px; }
        .method-tag.post { background-color: #4CAF50; }
        .method-tag.get { background-color: #2196F3; }
        .url { font-family: monospace; background-color: #e8eaf6; padding: 5px 10px; border-radius: 4px; font-size: 1.1em; color: #3f51b5; }
        .section-header { display: flex; align-items: center; margin-bottom: 15px; }
        .api-table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        .api-table th, .api-table td { border: 1px solid #ddd; padding: 8px; text-align: left; }
        .api-table th { background-color: #f7f7f7; }
        .required { color: red; font-weight: bold; }
        .code-block { background-color: #272822; color: #f8f8f2; padding: 10px; border-radius: 5px; overflow-x: auto; margin-top: 10px; }
    </style>
</head>
<body>

    <h1>Attendance System API Endpoints</h1>

    <h2>🧑‍💻 Employee Attendance Routes</h2>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag post">POST</span>
            <span class="url">/api/attendance/checkin</span>
        </div>
        <p>Marks the user's attendance check-in for the current day. **Requires Authentication.**</p>
        <h3>Response (Status: 200 OK)</h3>
        <div class="code-block"><pre>{ "success": true, "message": "Checked in successfully.", "checkInTime": "08:59 AM" }</pre></div>
    </div>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag post">POST</span>
            <span class="url">/api/attendance/checkout</span>
        </div>
        <p>Marks the user's attendance check-out for the current day. **Requires Authentication.**</p>
        <h3>Response (Status: 200 OK)</h3>
        <div class="code-block"><pre>{ "success": true, "message": "Checked out successfully.", "checkOutTime": "05:01 PM", "totalHours": 8.02 }</pre></div>
    </div>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag get">GET</span>
            <span class="url">/api/attendance/my-history</span>
        </div>
        <p>Retrieves all attendance records for the authenticated employee.</p>
        <h3>Query Parameters (Optional)</h3>
        <table class="api-table">
            <tr><th>Parameter</th><th>Type</th><th>Description</th></tr>
            <tr><td>month</td><td>integer</td><td>Filter by specific month (1-12).</td></tr>
            <tr><td>year</td><td>integer</td><td>Filter by specific year.</td></tr>
        </table>
    </div>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag get">GET</span>
            <span class="url">/api/attendance/my-summary</span>
        </div>
        <p>Retrieves the monthly summary (Present, Absent, Late counts) for the employee.</p>
    </div>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag get">GET</span>
            <span class="url">/api/attendance/today</span>
        </div>
        <p>Gets the current day's attendance status and times for the employee.</p>
    </div>

    <hr/>

    <h2>👑 Manager Attendance & Reporting Routes</h2>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag get">GET</span>
            <span class="url">/api/attendance/all</span>
        </div>
        <p>Retrieves all attendance records for all employees (filterable by date range/department).</p>
    </div>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag get">GET</span>
            <span class="url">/api/attendance/employee/:id</span>
        </div>
        <p>Retrieves the attendance history for a **specific employee** based on their user ID or Employee ID.</p>
    </div>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag get">GET</span>
            <span class="url">/api/attendance/summary</span>
        </div>
        <p>Retrieves the **Team Summary** (aggregated stats across all employees).</p>
    </div>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag get">GET</span>
            <span class="url">/api/attendance/export</span>
        </div>
        <p>Generates and initiates download of a CSV file for filtered attendance data.</p>
        <h3>Query Parameters (Required)</h3>
        <table class="api-table">
            <tr><th>Parameter</th><th>Type</th><th>Description</th></tr>
            <tr><td>startDate</td><td>date</td><td>Start date for the report.</td></tr>
            <tr><td>endDate</td><td>date</td><td>End date for the report.</td></tr>
        </table>
    </div>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag get">GET</span>
            <span class="url">/api/attendance/today-status</span>
        </div>
        <p>Lists all employees and their check-in status for the current day (e.g., used for "List of absent employees today" feature).</p>
    </div>

    <hr/>

    <h2>📊 Dashboard Routes</h2>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag get">GET</span>
            <span class="url">/api/dashboard/employee</span>
        </div>
        <p>Retrieves all data needed to populate the **Employee Dashboard** (Today's status, Monthly stats, Recent history).</p>
    </div>

    <div class="endpoint">
        <div class="section-header">
            <span class="method-tag get">GET</span>
            <span class="url">/api/dashboard/manager</span>
        </div>
        <p>Retrieves all data needed to populate the **Manager Dashboard** (Total employees, Today's counts, Charts data).</p>
    </div>

</body>
</html>

<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Запись к врачу</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Запись к врачу</h1>
        <form id="appointmentForm">
            <input type="text" id="patientName" placeholder="ФИО пациента" required />
            <input type="text" id="doctorName" placeholder="ФИО врача" required />
            <input type="date" id="appointmentDate" required />
            <button type="submit">Записаться</button>
        </form>
        <h2>Записи</h2>
        <div id="appointments"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>


body {
    font-family: Arial, sans-serif;
    background-color: #f5f5f5;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h1, h2 {
    text-align: center;
}

form {
    margin-bottom: 20px;
}

input {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%;
    margin-bottom: 10px;
}

button {
    padding: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    width: 100%;
}

button:hover {
    background-color: #0056b3;
}

.appointment-item {
    background: #e8f0fe;
    padding: 10px;
    margin: 10px 0;
    border-radius: 4px;
}

document.getElementById("appointmentForm").addEventListener("submit", function(event) {
    event.preventDefault();
    
    const patientName = document.getElementById("patientName").value;
    const doctorName = document.getElementById("doctorName").value;
    const appointmentDate = document.getElementById("appointmentDate").value;

    addAppointment(patientName, doctorName, appointmentDate);

    // Сбрасываем форму после добавления записи
    this.reset();
});

let appointments = [];

function addAppointment(patientName, doctorName, date) {
    const appointment = {
        patientName: patientName,
        doctorName: doctorName,
        date: date
    };
    
    appointments.push(appointment);
    displayAppointments();
}

function displayAppointments() {
    const appointmentsDiv = document.getElementById("appointments");
    appointmentsDiv.innerHTML = "";

    appointments.forEach((appointment, index) => {
        const appointmentElement = document.createElement("div");
        appointmentElement.className = "appointment-item";
        appointmentElement.innerHTML = `
            <strong>Пациент:</strong> ${appointment.patientName}<br>
            <strong>Врач:</strong> ${appointment.doctorName}<br>
            <strong>Дата:</strong> ${appointment.date}<br>
            <button onclick="removeAppointment(${index})">Удалить</button>
        `;
        appointmentsDiv.appendChild(appointmentElement);
    });
}

function removeAppointment(index) {
    appointments.splice(index, 1);
    displayAppointments();
}

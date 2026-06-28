<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bikash Catering - Booking</title>
    <style>
        /* Base & Mobile-First Reset */
        :root {
            --teal: #008080;
            --teal-light: #e6f2f2;
            --teal-dark: #006666;
            --bg: #f4f7f6;
            --text: #333333;
            --text-light: #666666;
            --border: #e0e5e3;
        }

        * {
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
        }

        /* Container */
        .container {
            background: #ffffff;
            width: 100%;
            max-width: 480px;
            border-radius: 20px;
            padding: 30px 24px;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.06);
            margin-top: 20px;
        }

        /* Header */
        .header {
            text-align: center;
            margin-bottom: 24px;
        }

        .header h1 {
            color: var(--teal);
            font-size: 28px;
            font-weight: 800;
            letter-spacing: -0.5px;
            margin-bottom: 6px;
        }

        .header p {
            color: var(--text-light);
            font-size: 15px;
        }

        /* Progress Bar */
        .progress-container {
            width: 100%;
            height: 6px;
            background: var(--border);
            border-radius: 10px;
            margin-bottom: 30px;
            overflow: hidden;
        }

        .progress-bar {
            height: 100%;
            width: 25%;
            background: var(--teal);
            border-radius: 10px;
            transition: width 0.4s ease;
        }

        /* Steps */
        .step {
            display: none;
            animation: fadeIn 0.3s ease;
        }

        .step.active {
            display: block;
        }

        .step-title {
            font-size: 20px;
            font-weight: 600;
            margin-bottom: 20px;
        }

        /* Tap-friendly Cards */
        .card {
            border: 2px solid var(--border);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 16px;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #fff;
        }

        .card:active {
            transform: scale(0.98);
        }

        .card:hover {
            border-color: var(--teal);
            background: var(--teal-light);
        }

        .card-info h3 {
            font-size: 18px;
            margin-bottom: 4px;
        }

        .card-info p {
            color: var(--text-light);
            font-size: 14px;
        }

        .card-price {
            font-size: 20px;
            font-weight: 700;
            color: var(--teal);
        }

        /* Form Inputs */
        .input-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            font-size: 14px;
            color: var(--text-light);
        }

        input {
            width: 100%;
            padding: 16px;
            border: 2px solid var(--border);
            border-radius: 12px;
            font-size: 16px;
            outline: none;
            transition: border-color 0.2s;
        }

        input:focus {
            border-color: var(--teal);
        }

        /* Buttons */
        .nav-buttons {
            display: flex;
            gap: 12px;
            margin-top: 30px;
        }

        button {
            flex: 1;
            padding: 18px;
            border-radius: 14px;
            font-size: 16px;
            font-weight: 700;
            border: none;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .btn-primary {
            background: var(--teal);
            color: #ffffff;
        }

        .btn-primary:active {
            background: var(--teal-dark);
            transform: scale(0.98);
        }

        .btn-secondary {
            background: var(--border);
            color: var(--text);
            flex: 0.4;
            display: none; /* Hidden on step 1 */
        }

        .btn-secondary:active {
            background: #d1d8d5;
            transform: scale(0.98);
        }

        /* Summary Screen */
        .success-icon {
            width: 64px;
            height: 64px;
            background: var(--teal-light);
            color: var(--teal);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
            margin: 0 auto 20px auto;
        }

        .summary-box {
            background: var(--bg);
            border-radius: 16px;
            padding: 20px;
            margin-top: 20px;
        }

        .summary-row {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid var(--border);
        }

        .summary-row:last-child {
            border-bottom: none;
        }

        .summary-label {
            color: var(--text-light);
            font-size: 14px;
        }

        .summary-value {
            font-weight: 600;
            font-size: 15px;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <div class="container">
        <div class="header">
            <h1>Bikash catering</h1>
            <p>Exceptional restaurant dining experiences</p>
        </div>

        <div class="progress-container" id="progress-container">
            <div class="progress-bar" id="progress-bar"></div>
        </div>

        <div class="step active" id="step-1">
            <h2 class="step-title">Select a service</h2>
            
            <div class="card" onclick="selectService('Breakfast', '8 AM to 9 AM', '$35')">
                <div class="card-info">
                    <h3>Breakfast</h3>
                    <p>8 AM to 9 AM</p>
                </div>
            </div>

            <div class="card" onclick="selectService('Lunch', '1 PM to 2 PM', '$60')">
                <div class="card-info">
                    <h3>Lunch</h3>
                    <p>1 PM to 2 PM</p>
                </div>
            </div>

            <div class="card" onclick="selectService('Dinner', '8 PM to 9 PM', '$50')">
                <div class="card-info">
                    <h3>Dinner</h3>
                    <p>8 PM to 9 PM</p>
                </div>
            </div>
        </div>

        <div class="step" id="step-2">
            <h2 class="step-title">Confirm price</h2>
            <p style="color: #666; margin-bottom: 16px;">Select the pricing for your chosen service.</p>
            
            <div class="card" onclick="nextStep()">
                <div class="card-info">
                    <h3 id="display-service-name">Service Name</h3>
                    <p id="display-service-time">Time</p>
                </div>
                <div class="card-price" id="display-service-price">$0</div>
            </div>
        </div>

        <div class="step" id="step-3">
            <h2 class="step-title">Your details</h2>
            
            <div class="input-group">
                <label for="name">Full Name</label>
                <input type="text" id="name" placeholder="John Doe" required>
            </div>

            <div class="input-group">
                <label for="phone">Phone Number</label>
                <input type="tel" id="phone" placeholder="(555) 000-0000" required>
            </div>
        </div>

        <div class="step" id="step-4">
            <div style="text-align: center;">
                <div class="success-icon">✓</div>
                <h2 class="step-title" style="margin-bottom: 8px;">Booking confirmed!</h2>
                <p style="color: var(--text-light);">We've saved your spot. See you soon!</p>
            </div>

            <div class="summary-box">
                <div class="summary-row">
                    <span class="summary-label">Name</span>
                    <span class="summary-value" id="summary-name">-</span>
                </div>
                <div class="summary-row">
                    <span class="summary-label">Service</span>
                    <span class="summary-value" id="summary-service">-</span>
                </div>
                <div class="summary-row">
                    <span class="summary-label">Time</span>
                    <span class="summary-value" id="summary-time">-</span>
                </div>
                <div class="summary-row">
                    <span class="summary-label">Total Price</span>
                    <span class="summary-value" id="summary-price" style="color: var(--teal);">-</span>
                </div>
            </div>
        </div>

        <div class="nav-buttons" id="nav-buttons">
            <button class="btn-secondary" id="btn-back" onclick="prevStep()">Back</button>
            <button class="btn-primary" id="btn-next" onclick="nextStep()" style="display: none;">Continue</button>
        </div>
    </div>

    <script>
        let currentStep = 1;
        const totalSteps = 4;

        // Booking Data Object
        let bookingData = {
            service: "",
            time: "",
            price: "",
            name: "",
            phone: ""
        };

        // Step 1: User taps a service card
        function selectService(serviceName, serviceTime, servicePrice) {
            bookingData.service = serviceName;
            bookingData.time = serviceTime;
            bookingData.price = servicePrice;
            
            // Populate step 2 data
            document.getElementById('display-service-name').innerText = serviceName;
            document.getElementById('display-service-time').innerText = serviceTime;
            document.getElementById('display-service-price').innerText = servicePrice;
            
            nextStep();
        }

        // Navigate forward
        function nextStep() {
            // Validation for Step 3
            if (currentStep === 3) {
                const nameInput = document.getElementById('name').value.trim();
                const phoneInput = document.getElementById('phone').value.trim();
                
                if (nameInput === "" || phoneInput === "") {
                    alert("Please enter both your name and phone number to confirm your booking.");
                    return;
                }
                bookingData.name = nameInput;
                bookingData.phone = phoneInput;
                populateSummary();
            }

            if (currentStep < totalSteps) {
                currentStep++;
                updateUI();
            }
        }

        // Navigate backward
        function prevStep() {
            if (currentStep > 1) {
                currentStep--;
                updateUI();
            }
        }

        // Populate final screen
        function populateSummary() {
            document.getElementById('summary-name').innerText = bookingData.name;
            document.getElementById('summary-service').innerText = bookingData.service;
            document.getElementById('summary-time').innerText = bookingData.time;
            document.getElementById('summary-price').innerText = bookingData.price;
        }

        // Update Interface visibility
        function updateUI() {
            // Hide all steps, show current step
            document.querySelectorAll('.step').forEach(step => step.classList.remove('active'));
            document.getElementById('step-' + currentStep).classList.add('active');

            // Update Progress Bar
            const progress = (currentStep / totalSteps) * 100;
            document.getElementById('progress-bar').style.width = progress + '%';

            // Manage Buttons
            const btnBack = document.getElementById('btn-back');
            const btnNext = document.getElementById('btn-next');
            const navButtons = document.getElementById('nav-buttons');
            const progressContainer = document.getElementById('progress-container');

            // Show/Hide Back Button
            btnBack.style.display = (currentStep === 1 || currentStep === totalSteps) ? 'none' : 'block';

            // Next button logic
            if (currentStep === 3) {
                btnNext.style.display = 'block';
                btnNext.innerText = 'Confirm Booking';
            } else {
                btnNext.style.display = 'none';
            }

            // Hide nav and progress bar completely on success screen (Step 4)
            if (currentStep === totalSteps) {
                navButtons.style.display = 'none';
                progressContainer.style.display = 'none';
            }
        }
    </script>

</body>
</html>

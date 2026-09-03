# revenue-leak-detective
AI-powered e-commerce revenue recovery system that detects cart abandonment, predicts purchase intent, identifies revenue opportunities, and integrates Razorpay for payment recovery.
# Revenue Leak Detective

### AI-based Revenue Recovery System for E-commerce

Revenue Leak Detective is a project built to identify customers who are likely to leave without completing a purchase and estimate the revenue that could potentially be recovered from them.

The system uses customer activity and purchase data to find patterns such as repeated cart abandonment, high-value carts, and previous purchase behaviour. Based on these patterns, it gives each customer a priority level and suggests a suitable recovery action.

The project also includes a Razorpay Test Mode payment flow to demonstrate how a potential recovery opportunity can be converted into a payment.

---

## Problem

In an e-commerce business, not every customer who adds a product to the cart completes the purchase.

For example, a customer may:

* Add products to the cart and leave
* Abandon the cart multiple times
* Spend a lot of time browsing but not purchase
* Have a high-value cart but never complete payment
* Return to the website several times without converting

Looking at these customers manually is difficult when there are thousands of sessions.

The main question this project tries to answer is:

> **Which customers are worth targeting for recovery, and how much revenue could potentially be recovered?**

---

## Solution

Revenue Leak Detective takes e-commerce activity data and processes it at the customer level.

The basic workflow is:

```text
E-commerce Data
      ↓
Data Processing
      ↓
Customer-level Features
      ↓
Machine Learning Model
      ↓
Purchase Probability
      ↓
Revenue Opportunity
      ↓
Priority & Reason
      ↓
Recommended Recovery Action
      ↓
Razorpay Payment
```

The idea is to combine the ML prediction with business rules so that the output is useful for an e-commerce team rather than being just a model prediction.

---

## How It Works

### 1. Customer Data

The project uses an e-commerce dataset containing information about customer sessions, products, carts, purchases, revenue and other behaviour.

Some of the important fields include:

* Customer ID
* Session ID
* Product
* Product category
* Unit price
* Quantity
* Discount
* Revenue
* Pages viewed
* Time spent on site
* Added to cart
* Purchased
* Cart abandoned
* Payment method
* Location

---

### 2. Customer Aggregation

Instead of looking at every session separately, the data is combined to create customer-level information.

For example:

```text
Customer ID
Total Revenue
Total Sessions
Total Carts
Total Purchases
Abandoned Carts
Average Order Value
Average Discount
Average Time on Site
```

This gives a better view of the customer's overall behaviour.

---

### 3. Purchase Prediction

Machine learning is used to estimate the probability that a customer will complete a purchase.

The project experiments with different ML approaches and uses the trained model to generate predictions.

The prediction is then used along with customer behaviour to identify possible recovery opportunities.

---

### 4. Revenue Opportunity

The system also estimates the potential revenue associated with a customer.

For example:

```text
Customer: 1985

Historical Revenue: ₹4,485.96
Abandoned Sessions: 5
Purchase Probability: 43.35%
Potential Revenue Opportunity: ₹7,271.92
```

This helps in deciding which customers should receive more attention.

---

### 5. Priority

Customers are grouped into different priority levels based on their behaviour and estimated opportunity.

```text
HIGH
MEDIUM
LOW
```

For example, a customer with repeated cart abandonment and a large potential order may receive a higher priority than a customer with very little activity.

---

### 6. Reason for the Flag

The system provides simple reasons for why a customer was selected.

Example:

```text
Customer has repeatedly abandoned carts

Large potential revenue opportunity
```

This makes the result easier to understand instead of showing only a probability value.

---

### 7. Recommended Action

Based on the customer's situation, the system can recommend a recovery action.

For example:

```text
Target customer for recovery
Offer an appropriate incentive
Send a recovery reminder
Create a payment order
```

The purpose is to connect the ML output with a practical business action.

---

# Razorpay Integration

Razorpay Test Mode is used to demonstrate the payment part of the recovery process.

The flow is:

```text
Customer Selected for Recovery
            ↓
Recovery Action
            ↓
Create Razorpay Order
            ↓
Customer Payment
            ↓
Payment Verification
            ↓
Recovery Status Updated
```

The project uses test credentials during development, so no real payment is required.

After a successful payment, the recovery status is updated so that the customer is not unnecessarily targeted again.

---

# Example

Suppose a customer has:

```text
5 abandoned sessions
₹7,271 estimated opportunity
43.35% purchase probability
```

The system can flag the customer as a high-priority recovery opportunity.

Instead of simply displaying the customer in a dashboard, the system provides:

```text
Priority:
HIGH

Reason:
Repeated cart abandonment
Large potential revenue opportunity

Suggested Action:
Target customer for recovery
```

The recovery flow can then be connected to a Razorpay payment order.

---

# Dashboard

The frontend provides a dashboard for viewing the results.

It includes information such as:

* Total revenue
* Customer activity
* Abandoned carts
* Revenue opportunities
* Purchase probability
* Customer priority
* Reasons for detection
* Recommended actions
* Recovery/payment status

The dashboard is intended to give an e-commerce team a simple way to identify where potential revenue is being lost.

---

# Technology Used

### Frontend

* React
* Vite
* JavaScript
* CSS

### Backend

* Python
* FastAPI
* REST APIs

### Machine Learning

* Pandas
* NumPy
* Scikit-learn
* XGBoost

### Payment

* Razorpay Test Mode

### Database / Data

* E-commerce dataset
* Customer-level aggregation

---

# Project Structure

```text
Revenue_Leak_Detective/
│
├── frontend/
│   ├── src/
│   ├── package.json
│   ├── package-lock.json
│   ├── vite.config.js
│   └── index.html
│
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── ml.py
│   │   ├── agent.py
│   │   ├── payment.py
│   │   ├── models.py
│   │   ├── db.py
│   │   ├── schemas.py
│   │   └── config.py
│   │
│   ├── data/
│   │   └── Ecommerce.csv
│   │
│   ├── requirements.txt
│   └── .env.example
│
├── README.md
├── run_backend.bat
└── run_frontend.bat
```

---

# Setup

## Backend

Create a virtual environment:

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Install the required packages:

```bash
pip install -r backend/requirements.txt
```

Run the backend:

```bash
uvicorn backend.app.main:app --reload
```

The API will run locally on:

```text
http://127.0.0.1:8000
```

API documentation is available at:

```text
http://127.0.0.1:8000/docs
```

---

## Frontend

Open another terminal:

```bash
cd frontend
```

Install dependencies:

```bash
npm install
```

Run the frontend:

```bash
npm run dev
```

Open the local URL displayed by Vite.

---

# Environment Variables

Create a `.env` file for the backend and add your Razorpay test credentials.

```env
RAZORPAY_KEY_ID=your_test_key_id
RAZORPAY_KEY_SECRET=your_test_key_secret
```

Do not upload the actual `.env` file to GitHub.

Use `.env.example` as the template.

---

# Current Project Capabilities

* Customer-level e-commerce analysis
* Cart abandonment detection
* Purchase probability prediction
* Revenue opportunity estimation
* Customer prioritization
* Reason identification
* Recovery action recommendation
* Razorpay Test Mode integration
* Payment verification
* Recovery status tracking
* Web-based dashboard

---

# Future Improvements

Some possible improvements for the next version are:

* Real-time customer behaviour tracking
* Better personalization of recovery offers
* Integration with email/SMS/WhatsApp campaigns
* More advanced customer segmentation
* A/B testing of recovery strategies
* Continuous model retraining using new transaction data
* Detailed recovery ROI tracking
* Production payment integration

---

# Project Goal

The goal of Revenue Leak Detective is not only to predict customer behaviour.

It is to connect the prediction with a practical recovery process:

```text
Detect → Understand → Prioritize → Act → Recover
```

This demonstrates how machine learning and payment infrastructure can work together to address a real e-commerce problem.

---

## Built For

**Razorpay Ideathon / Buildathon**

### Project: Revenue Leak Detective

**Focus:** AI/ML + Agentic Commerce + Revenue Recovery + Payments

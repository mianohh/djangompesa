# M-Pesa Daraja API Integration (Django)

A simple Django app that integrates with the **Safaricom M-Pesa Daraja API** (sandbox) to
request an OAuth access token and trigger an **STK Push** (Lipa Na M-Pesa Online) payment.

## Features

- Get an M-Pesa OAuth access token
- Generate the STK Push password (Shortcode + Passkey + Timestamp, Base64 encoded)
- Initiate an STK Push payment to a phone number
- Secrets stored in a `.env` file instead of hardcoded in the source code

## Project Structure

```
mpesadaraja/
├── manage.py
├── .env                  # environment variables (never commit this)
├── .gitignore
├── requirements.txt
├── mpesadaraja/          # project settings
│   ├── settings.py
│   └── urls.py
└── myapp/
    ├── credentials.py    # M-Pesa API logic
    ├── views.py
    ├── urls.py
    ├── templates/        # home.html, pay.html, token.html, layout.html
    └── static/           # style.css
```

## Requirements

- Python 3.14+
- Django 6.1
- A Safaricom Daraja developer account (sandbox)

## Setup

### 1. Clone the repo and create a virtual environment

```bash
cd mpesadaraja
python -m venv venv
source venv/bin/activate
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Create your `.env` file

Create a file named `.env` in the project root (next to `manage.py`):

```ini
MPESA_CONSUMER_KEY=your_consumer_key_here
MPESA_CONSUMER_SECRET=your_consumer_secret_here
MPESA_SHORTCODE=your_shortcode_here
MPESA_PASSKEY=your_stk_push_passkey_here
```

Get these values from the [Daraja Developer Portal](https://developer.safaricom.co.ke)
after creating an app in the sandbox.



### 4. Run migrations and start the server

```bash
python manage.py migrate
python manage.py runserver
```

Visit: http://127.0.0.1:8000/

## Usage

| URL | Description |
|---|---|
| `/` | Home page |
| `/token` | Displays the current M-Pesa access token |
| `/pay` | Form to enter phone number and amount, then sends an STK push |
| `/stk` | Same payment form (STK push page) |
| `/admin/` | Django admin |

### STK Push request example

Send a `POST` request to `/pay` with:

| Field | Example |
|---|---|
| `phone` | `2547XXXXXXXX` |
| `amount` | `1` |



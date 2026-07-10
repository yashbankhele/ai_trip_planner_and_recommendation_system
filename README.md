# 🌍 AI Trip Planner & Hotel Booking

An AI-powered travel planning and hotel booking platform built with Django. It turns a destination, a date range, and a few preferences into a full day-by-day itinerary — complete with cost breakdowns, hotel suggestions, interactive maps, and weather — then lets users book a hotel and pay for it in the same flow.

![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)
![Django](https://img.shields.io/badge/Django-5.2-green.svg)
![AI](https://img.shields.io/badge/AI-Google%20Gemini%202.5%20Flash-orange.svg)
![License](https://img.shields.io/badge/License-Educational-lightgrey.svg)

## Table of Contents

- [Why this project is useful](#why-this-project-is-useful)
- [Tech stack](#tech-stack)
- [Getting started](#getting-started)
- [Usage](#usage)
- [Project structure](#project-structure)
- [Configuration](#configuration)
- [Getting help](#getting-help)
- [Maintainers & contributing](#maintainers--contributing)

## Why this project is useful

- **AI-generated itineraries** — [Google Gemini 2.5 Flash](https://ai.google.dev/docs) builds a personalized, day-by-day plan from destination, trip length, activities, travel companions, and start date, including cost estimates and local tips.
- **Hotel discovery & booking** — Browse hotels near a destination, view details, and complete a booking with an integrated [Razorpay](https://razorpay.com/docs/) payment flow.
- **Trip context, not just a list** — Live weather, an interactive [Folium](https://python-visualization.github.io/folium/) map, and nearby transportation options are surfaced alongside each destination.
- **Accounts & history** — Registration, login, profile editing, saved trips, and a feedback/review system are built in.

## Tech stack

| Layer | Technology |
|---|---|
| Backend | Django 5.2, Django REST Framework |
| Database | SQLite (default, dev-ready; swap `DATABASES` in `settings.py` for production) |
| AI | Google Generative AI (`google-generativeai`), Gemini 2.5 Flash |
| Payments | Razorpay |
| Maps | Folium / OpenStreetMap |
| Frontend | Django templates, CSS, vanilla JS |
| Email | SMTP (Gmail) |

## Getting started

### Prerequisites

- Python 3.12+
- A [Google Gemini API key](https://makersuite.google.com/app/apikey)
- A [Razorpay](https://razorpay.com/) account (test keys are fine for local development)

### Installation

```bash
# 1. Clone the repository
git clone <repository-url>
cd AI-trip-Planner-and-Hotel-booking-main

# 2. Create and activate a virtual environment
python -m venv venv
# Windows PowerShell:
.\venv\Scripts\Activate.ps1
# Windows CMD:
venv\Scripts\activate.bat
# macOS/Linux:
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Configure your API keys — see Configuration below

# 5. Apply database migrations
python manage.py migrate

# 6. Create an admin user
python manage.py createsuperuser

# 7. Run the development server
python manage.py runserver
```

Windows users can instead run the bundled `setup.ps1` (automated setup) or `start_server.bat` / `start_server.ps1` once configured.

The app is served at `http://127.0.0.1:8000/`, with the admin panel at `http://127.0.0.1:8000/admin/`.

For a more detailed walkthrough, see [INSTALLATION.md](INSTALLATION.md) and [CONFIG_CHECKLIST.md](CONFIG_CHECKLIST.md).

## Usage

Once the server is running:

1. Register an account (or log in as the superuser you created).
2. Go to **Plan a Trip**, enter a destination, dates, activities, and companions, and generate an AI itinerary.
3. Browse hotels near your destination, check details, and complete a booking through the Razorpay checkout.
4. Check the weather and interactive map for your destination, and view nearby transportation options.
5. Save trips to your profile and leave feedback afterward.

You can also call the AI trip generator directly from a Django shell:

```bash
python manage.py shell
```

```python
from hotels.gemini_ai import generate_trip_plan
result = generate_trip_plan("Paris", 5, "museums", "solo", "2026-06-01")
```

## Project structure

```
AI-trip-Planner-and-Hotel-booking-main/
├── TravelandHotelBooking/   # Django project settings, URLs, WSGI/ASGI config
├── accounts/                 # Auth, profiles, feedback (models, views, forms)
├── hotels/                   # Core app: places, hotels, bookings, gemini_ai.py
├── templates/                # Django templates (accounts/, hotels/)
├── static/                   # CSS, JS, fonts, images
├── media/                    # User-uploaded and seed images
├── manage.py                 # Django management CLI
├── requirements.txt          # Python dependencies
└── INSTALLATION.md           # Detailed setup guide
```

## Configuration

API keys and credentials live in `TravelandHotelBooking/settings.py`:

```python
# Google Gemini AI
GEMINI_API_KEY = "your-gemini-api-key"
GEMINI_MODEL_NAME = "models/gemini-2.5-flash"

# Razorpay Payments
RAZORPAY_KEY_ID = "your-razorpay-key-id"
RAZORPAY_KEY_SECRET = "your-razorpay-secret"

# Email (SMTP)
EMAIL_HOST_USER = "your-email@gmail.com"
EMAIL_HOST_PASSWORD = "your-app-password"
```

> **Note:** This repo currently ships with real-looking keys committed directly in `settings.py` for ease of local setup. Before deploying or pushing to a public repository, move these to environment variables (e.g. via `python-decouple` or `django-environ`), rotate any keys that were ever committed, and set `DEBUG = False` with a real `ALLOWED_HOSTS` list.

Common Django management commands:

```bash
python manage.py makemigrations   # Create migrations after model changes
python manage.py migrate          # Apply migrations
python manage.py collectstatic    # Collect static files for production
python manage.py test             # Run the test suite
```

## Getting help

- Start with [INSTALLATION.md](INSTALLATION.md) and [CONFIG_CHECKLIST.md](CONFIG_CHECKLIST.md) for setup issues.
- [PROJECT_DEEP_DIVE.md](PROJECT_DEEP_DIVE.md) covers how the app fits together internally.
- [EMERGENCY_COMMANDS.txt](EMERGENCY_COMMANDS.txt) has quick fixes for common local dev problems.
- External docs: [Django](https://docs.djangoproject.com/), [Gemini API](https://ai.google.dev/docs), [Razorpay API](https://razorpay.com/docs/).

## Maintainers & contributing

This project is maintained as an educational/portfolio project. Issues and pull requests are welcome:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes and open a pull request

This project is licensed for educational purposes.

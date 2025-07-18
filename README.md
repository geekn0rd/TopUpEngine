# TopUpEngine
A robust B2B credit and recharge system with secure top-up requests, atomic transactions, and audit-safe accounting under high-concurrency load. Built with Django.

---

## 🚀 Features
- **Seller Management** – Each seller has a credit balance.
- **Top-Up Requests** – Sellers request credit; admins approve.
- **Recharge API** – Deducts credit and logs transactions for phone number recharge.
- **Atomic Transactions** – Prevents race conditions and double-spending.
- **Audit Logging** – Every top-up and recharge is logged for reconciliation.
- **Concurrency Safety** – Handles high parallel load with DB-level row locking.
- **Idempotent Operations** – Top-up requests cannot be approved twice.
- **Test Coverage** – Includes unit tests and load/concurrency tests.

---

## 🏗 Architecture
- **Seller**: Holds balance, never negative.
- **PhoneNumber**: Optional ownership by sellers.
- **TopUpRequest**: Represents credit-increase requests.
- **TransactionLog**: Tracks all credit changes for accounting.

---

## 📦 Tech Stack
- **Backend**: Django, Django REST Framework
- **Database**: PostgreSQL (for row-level locking)
- **Testing**: Django Test Framework, threading for concurrency tests

---

## 🔑 API Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/topup/` | Create top-up request |
| `POST` | `/api/topup/<uuid>/approve/` | Admin approves top-up |
| `POST` | `/api/recharge/` | Recharge phone number & deduct credit |

---

## 🛡 Key Guarantees
- No negative balances
- Double-spend prevention
- Atomic DB transactions
- Audit reconciliation always matches

---

## ▶️ Quick Start
```bash
# Clone the repository
git clone https://github.com/your-username/TopUpEngine.git
cd TopUpEngine

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Apply migrations
python manage.py migrate

# Run server
python manage.py runserver

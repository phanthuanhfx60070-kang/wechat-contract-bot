# WeChat Contract Bot

A powerful WeChat bot application designed to automate contract management, processing, and notifications. This bot streamlines contract workflows and improves team collaboration through WeChat messaging.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)
- [License](#license)
- [Support](#support)

## 🎯 Overview

WeChat Contract Bot is a comprehensive solution for managing contracts through WeChat. It integrates with WeChat's API to provide real-time notifications, contract tracking, and automated workflows. The bot helps teams manage contract lifecycles more efficiently by providing instant updates and quick access to contract information directly within WeChat.

### Key Benefits

- **Real-time Notifications**: Instant contract status updates via WeChat
- **Automated Workflows**: Streamline contract approval and processing
- **Easy Access**: Quick contract lookup and information retrieval
- **Team Collaboration**: Simplified communication around contracts
- **Audit Trail**: Complete tracking of contract interactions

## ✨ Features

### Core Features

- **Contract Management**
  - Create, update, and delete contracts
  - Track contract status and lifecycle
  - Store contract metadata and attachments
  - Version control for contract documents

- **WeChat Integration**
  - Direct messaging with the bot
  - Group chat support
  - Rich message formatting
  - Interactive buttons and menus

- **Notifications & Alerts**
  - Contract expiration reminders
  - Status change notifications
  - Approval request alerts
  - Custom notification rules

- **User Management**
  - Role-based access control
  - User authentication
  - Permission management
  - Activity logging

- **Reporting & Analytics**
  - Contract analytics dashboard
  - Performance metrics
  - Export capabilities
  - Custom report generation

## 📦 Prerequisites

Before setting up the WeChat Contract Bot, ensure you have the following installed:

- **Python** 3.8 or higher
- **pip** (Python package manager)
- **Git** for version control
- **WeChat Official Account** (for bot deployment)
- **MySQL** or **PostgreSQL** (for database)
- **Redis** (optional, for caching and session management)

### System Requirements

- **OS**: Linux, macOS, or Windows
- **Memory**: Minimum 2GB RAM
- **Storage**: Minimum 5GB free space
- **Network**: Stable internet connection

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/phanthuanhfx60070-kang/wechat-contract-bot.git
cd wechat-contract-bot
```

### 2. Create Virtual Environment

```bash
# On Windows
python -m venv venv
venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Set Up Database

```bash
# Create database
python manage.py migrate

# Create superuser (for admin access)
python manage.py createsuperuser
```

### 5. Configure Environment Variables

Create a `.env` file in the project root:

```bash
cp .env.example .env
```

Edit `.env` with your configuration:

```env
# WeChat Configuration
WECHAT_APPID=your_wechat_app_id
WECHAT_APPSECRET=your_wechat_app_secret
WECHAT_TOKEN=your_wechat_token
WECHAT_ENCODINGAESKEY=your_encoding_aes_key

# Database Configuration
DATABASE_URL=mysql://user:password@localhost/wechat_contract_bot
REDIS_URL=redis://localhost:6379/0

# Application Settings
DEBUG=False
SECRET_KEY=your_secret_key
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com

# Email Configuration (Optional)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_HOST_USER=your_email@gmail.com
EMAIL_HOST_PASSWORD=your_email_password
```

## ⚙️ Configuration

### WeChat Official Account Setup

1. **Register WeChat Official Account** at [https://mp.weixin.qq.com](https://mp.weixin.qq.com)
2. **Enable Developer Mode**:
   - Go to Settings → Basic Information
   - Enable "Developer Mode"
   - Set Callback URL to: `https://yourdomain.com/api/wechat/callback`
   - Set Token and EncodingAESKey
3. **Create Menu** (Optional):
   - Configure custom menus for quick access to bot features

### Database Configuration

For MySQL:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'wechat_contract_bot',
        'USER': 'root',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

For PostgreSQL:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'wechat_contract_bot',
        'USER': 'postgres',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

## 📖 Usage

### Starting the Bot

```bash
# Run development server
python manage.py runserver

# Run production server (with Gunicorn)
gunicorn wechat_contract_bot.wsgi:application --bind 0.0.0.0:8000
```

### Basic Commands

Users can interact with the bot using these commands in WeChat:

```
# View all available commands
/help

# Create a new contract
/contract create [contract_name]

# View contract details
/contract view [contract_id]

# Update contract status
/contract status [contract_id] [new_status]

# List all contracts
/contracts list

# Search contracts
/search [keyword]

# Get notifications settings
/settings
```

### Web Dashboard

Access the admin dashboard at `http://localhost:8000/admin/` with your superuser credentials.

### API Endpoints

- **Contracts**
  - `GET /api/contracts/` - List all contracts
  - `POST /api/contracts/` - Create new contract
  - `GET /api/contracts/<id>/` - Get contract details
  - `PUT /api/contracts/<id>/` - Update contract
  - `DELETE /api/contracts/<id>/` - Delete contract

- **WeChat Messages**
  - `POST /api/wechat/messages/` - Send message
  - `GET /api/wechat/messages/` - Get message history

## 📁 Project Structure

```
wechat-contract-bot/
├── manage.py                 # Django management script
├── requirements.txt          # Python dependencies
├── .env.example             # Example environment variables
├── .gitignore               # Git ignore file
├── README.md                # This file
│
├── wechat_contract_bot/     # Main project folder
│   ├── settings.py          # Project settings
│   ├── urls.py              # URL routing
│   ├── wsgi.py              # WSGI configuration
│   └── __init__.py
│
├── contracts/               # Contracts app
│   ├── models.py            # Contract models
│   ├── views.py             # Views and business logic
│   ├── serializers.py       # DRF serializers
│   ├── urls.py              # App URL routing
│   ├── admin.py             # Admin configuration
│   └── migrations/          # Database migrations
│
├── wechat/                  # WeChat integration app
│   ├── models.py            # WeChat message models
│   ├── handlers.py          # Message handlers
│   ├── views.py             # WeChat API views
│   ├── urls.py              # App URL routing
│   ├── utils.py             # Utility functions
│   └── migrations/          # Database migrations
│
├── users/                   # User management app
│   ├── models.py            # User models
│   ├── views.py             # Authentication views
│   ├── serializers.py       # DRF serializers
│   ├── urls.py              # App URL routing
│   └── migrations/          # Database migrations
│
├── notifications/           # Notifications app
│   ├── models.py            # Notification models
│   ├── tasks.py             # Celery tasks
│   ├── views.py             # Notification views
│   └── urls.py              # App URL routing
│
└── static/                  # Static files
    ├── css/                 # Stylesheets
    ├── js/                  # JavaScript files
    └── img/                 # Images
```

## 📚 API Documentation

### Contracts API

#### List Contracts

```http
GET /api/contracts/
```

**Query Parameters:**
- `status` - Filter by status (draft, pending, approved, signed, archived)
- `created_after` - Filter by creation date
- `search` - Search by contract name or ID

**Response:**
```json
{
  "count": 10,
  "next": null,
  "previous": null,
  "results": [
    {
      "id": 1,
      "name": "Service Agreement",
      "status": "signed",
      "created_at": "2026-01-14T04:36:48Z",
      "updated_at": "2026-01-14T04:36:48Z"
    }
  ]
}
```

#### Create Contract

```http
POST /api/contracts/
Content-Type: application/json

{
  "name": "New Contract",
  "description": "Contract description",
  "parties": ["Party A", "Party B"],
  "start_date": "2026-01-14",
  "end_date": "2027-01-14",
  "amount": 10000.00
}
```

#### Get Contract Details

```http
GET /api/contracts/{id}/
```

#### Update Contract

```http
PUT /api/contracts/{id}/
Content-Type: application/json

{
  "status": "approved",
  "updated_by": "user_id"
}
```

#### Delete Contract

```http
DELETE /api/contracts/{id}/
```

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Commit your changes** (`git commit -m 'Add amazing feature'`)
4. **Push to the branch** (`git push origin feature/amazing-feature`)
5. **Open a Pull Request**

### Coding Standards

- Follow PEP 8 style guide for Python
- Write docstrings for all functions and classes
- Add unit tests for new features
- Update documentation as needed

### Testing

```bash
# Run tests
python manage.py test

# Run tests with coverage
coverage run --source='.' manage.py test
coverage report
```

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 💬 Support

For questions, issues, or suggestions:

- **GitHub Issues**: [Create an issue](https://github.com/phanthuanhfx60070-kang/wechat-contract-bot/issues)
- **Email**: Contact the development team
- **Documentation**: Check the [Wiki](https://github.com/phanthuanhfx60070-kang/wechat-contract-bot/wiki)

### Troubleshooting

**Issue: WeChat API Connection Failed**
- Verify WECHAT_APPID and WECHAT_APPSECRET are correct
- Check firewall and network connectivity
- Ensure callback URL is publicly accessible

**Issue: Database Connection Error**
- Verify DATABASE_URL in .env file
- Check database server is running
- Ensure user has proper permissions

**Issue: Static Files Not Loading**
```bash
python manage.py collectstatic --noinput
```

## 🙏 Acknowledgments

- WeChat Official API documentation
- Django community
- Django REST Framework
- All contributors and users

---

**Last Updated**: January 14, 2026

**Version**: 1.0.0

For the latest updates, visit the [GitHub repository](https://github.com/phanthuanhfx60070-kang/wechat-contract-bot)

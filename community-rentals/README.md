<p align="center">
  <img src="./img.png" alt="CampusConnect Banner" width="100%">
</p>

# CampusConnect 🎓

## Basic Details

### Team Name: Hackstreet Girls

### Team Members
- Member 1: Alfia Fathima
- Member 2: Neha Babu

### Hosted Project Link
https://campus-rental.onrender.com/

### Project Description
CampusConnect is a comprehensive campus rental and microtask platform designed to connect students for seamless sharing, renting, and earning opportunities. The platform enables students to list items for rent, post microtasks for quick jobs, and build trust within their campus community through a reputation-based system.

### The Problem Statement
College students often need items temporarily (textbooks, electronics, sports equipment) but can't afford to buy them. Similarly, students looking for quick earning opportunities struggle to find small tasks or gigs within their campus. Existing platforms are either too formal, charge high fees, or lack the trust factor needed for peer-to-peer transactions in a campus setting.

### The Solution
CampusConnect provides a trusted, student-centric platform where peers can:
- **Rent items** from fellow students at affordable rates
- **Post and accept microtasks** for quick earning opportunities
- **Build trust scores** through successful transactions
- **Connect directly** within their campus community
- All in a professional, aesthetic, and easy-to-use interface designed specifically for students

---

## Technical Details

### Technologies/Components Used

**For Software:**
- **Languages:** Python 3.x, HTML5, CSS3, JavaScript
- **Framework:** Flask 3.0.0 (Python web framework)
- **Database:** SQLite3 (lightweight, file-based database)
- **Server:** Gunicorn 21.2.0 (WSGI HTTP Server)
- **UI Framework:** Custom CSS with modern design principles
- **Tools:** VS Code, Git, GitHub

**Tech Stack:**
```
Backend:  Flask (Python)
Database: SQLite3
Frontend: HTML5, CSS3, JavaScript
Server:   Gunicorn
Hosting:  Vercel/Render
```

---

## Features

### Core Features

**1. User Authentication & Trust System**
- Simple name and email-based registration
- Session management for secure access
- Trust score system (starts at 100, increases with completed tasks)
- User profile with reputation tracking

**2. Campus Rental Marketplace**
- Browse available items for rent
- List your own items with details (name, description, category, price per day)
- Search and filter by category
- View item availability status
- Direct connection with item owners

**3. Micro Tasks Platform**
- Post tasks with title, description, location, and reward amount
- Browse available tasks sorted by recency
- Accept tasks to work on
- Mark tasks as completed
- Task status tracking (open → accepted → completed)
- Earn trust points by completing tasks

**4. Trust & Reputation System**
- Every user starts with 100 trust points
- Earn +5 points for each completed task
- Trust scores visible to build community confidence
- Encourages responsible behavior and quality service

**5. Responsive Dashboard**
- Clean, modern interface with sky blue and white theme
- Quick access to rentals and microtasks through 3D widgets
- Real-time status updates
- Flash messages for user feedback

---

## Database Schema

### Users Table
```sql
users (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL,
    trust_score INTEGER DEFAULT 100
)
```

### Tasks Table
```sql
tasks (
    id INTEGER PRIMARY KEY,
    title TEXT NOT NULL,
    description TEXT NOT NULL,
    location TEXT,
    reward REAL NOT NULL,
    posted_by TEXT,
    accepted_by TEXT,
    status TEXT DEFAULT 'open',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
)
```

### Items Table
```sql
items (
    id INTEGER PRIMARY KEY,
    item_name TEXT NOT NULL,
    description TEXT,
    category TEXT,
    price_per_day REAL NOT NULL,
    owner_name TEXT,
    is_available BOOLEAN DEFAULT 1
)
```

---

## Implementation

### Installation

**Prerequisites:**
- Python 3.7 or higher
- pip (Python package manager)

**Step 1: Clone the Repository**
```bash
git clone https://github.com/alfiagit27/campus-rental.git
cd campus-rental/community-rentals
```

**Step 2: Create Virtual Environment (Recommended)**
```bash
# On Windows
python -m venv venv
venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

**Step 3: Install Dependencies**
```bash
pip install -r requirements.txt
```

**Step 4: Initialize Database**
The database will be automatically created on first run.

### Run

**Development Mode:**
```bash
python app.py
```

The application will be available at: `http://localhost:5000`

**Production Mode (with Gunicorn):**
```bash
gunicorn app:app --bind 0.0.0.0:5000
```

### Environment Variables

For production deployment, set:
```bash
export PORT=5000
export FLASK_ENV=production
```

---

## Project Documentation

### Application Routes

**Authentication:**
- `GET/POST /` - Login page (auto-registers new users)
- `GET /logout` - Clear session and logout

**Dashboard:**
- `GET /dashboard` - Main dashboard with trust score and widgets

**Rental Items:**
- `GET /items` - Browse all available rental items
- `GET/POST /list_item` - List a new item for rent

**Micro Tasks:**
- `GET /tasks` - Browse all posted tasks
- `GET/POST /post_task` - Post a new task
- `GET /accept_task/<id>` - Accept a task
- `GET /complete_task/<id>` - Mark task as completed (earns trust points)

### Screenshots

#### 1. Login Page


<img width="1918" height="1013" alt="Screenshot 2026-02-14 070020" src="https://github.com/user-attachments/assets/111a526b-75c5-4cce-9350-310e06eb4d30" />


#### 2. Dashboard


<img width="1898" height="940" alt="Screenshot 2026-02-14 070133" src="https://github.com/user-attachments/assets/d8453c11-4e06-4cb7-89c6-14fd8836cf58" />


#### 3. Browse Rental Items


<img width="1915" height="922" alt="Screenshot 2026-02-14 070242" src="https://github.com/user-attachments/assets/6b945302-82e3-4853-8503-9375558a5bcf" />

<img width="1919" height="974" alt="Screenshot 2026-02-14 070312" src="https://github.com/user-attachments/assets/eb16642e-0d95-451c-b137-6a057e58500f" />


<img width="667" height="540" alt="Screenshot 2026-02-14 070601" src="https://github.com/user-attachments/assets/afc6c86a-18a8-4e85-841b-190a90d30df9" />



#### 4. Micro Tasks
<img width="1919" height="936" alt="Screenshot 2026-02-14 070719" src="https://github.com/user-attachments/assets/d26f7bc7-96eb-462d-94c2-f50b3bb3101b" />





#### 5. Post Task Form
<img width="1865" height="968" alt="Screenshot 2026-02-14 070704" src="https://github.com/user-attachments/assets/ec4a2e18-a053-4b71-a06a-810a7e4bad41" />




### Application Workflow

```
┌─────────────┐
│ Login/Sign  │
│     Up      │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Dashboard  │◄───────────┐
│   (Trust    │            │
│   Score)    │            │
└──────┬──────┘            │
       │                   │
       ├────────┬──────────┤
       ▼        ▼          │
   ┌───────┐ ┌────────┐   │
   │ Rent  │ │ Micro  │   │
   │ Items │ │ Tasks  │   │
   └───┬───┘ └───┬────┘   │
       │         │         │
       ▼         ▼         │
  ┌────────┐ ┌─────────┐  │
  │ Browse │ │ Browse  │  │
  │ Items  │ │ Tasks   │  │
  └───┬────┘ └────┬────┘  │
      │           │        │
      ▼           ▼        │
  ┌────────┐ ┌─────────┐  │
  │  List  │ │  Post   │  │
  │  Item  │ │  Task   │  │
  └────────┘ └────┬────┘  │
                  │        │
                  ▼        │
              ┌────────┐   │
              │ Accept │   │
              │  Task  │   │
              └────┬───┘   │
                   │       │
                   ▼       │
              ┌─────────┐  │
              │Complete │  │
              │  Task   │──┘
              │(+5 Trust)│
              └─────────┘
```

---

## UI/UX Design Features

### Color Scheme
- **Primary:** Sky Blue (#87CEEB) - Professional and calming
- **Secondary:** White (#FFFFFF) - Clean and modern
- **Accent:** Yellow (#FFD700) - Highlights and CTAs with 3D effects
- **Text:** Dark Gray (#343A40) - High readability

### Design Principles
1. **Aesthetic & Professional** - Clean, modern interface suitable for college students
2. **3D Effects** - Widgets and buttons have smooth 3D hover transformations
3. **User-Friendly** - Intuitive navigation with clear visual hierarchy
4. **Responsive** - Works seamlessly on desktop, tablet, and mobile
5. **Consistent** - Unified theme across all pages

### Key UI Elements
- **Login Page:** Centered card with sky blue gradient background
- **Dashboard Widgets:** Yellow cards with 3D hover effects (lift, rotate, scale, glow)
- **Forms:** Professional input fields with smooth focus animations
- **Cards:** Clean white cards with sky blue accents and hover effects
- **Buttons:** Rounded with gradient backgrounds and transform effects

---

## Deployment



### Render Deployment

**1. Create `render.yaml` file:**
```yaml
services:
  - type: web
    name: campus-rental
    env: python
    buildCommand: "pip install -r requirements.txt"
    startCommand: "gunicorn app:app"
    envVars:
      - key: PYTHON_VERSION
        value: 3.9.0
```

**2. Push to GitHub and connect to Render**

---

## Project Demo

### Video
[Add your demo video link here - YouTube, Google Drive, etc.]

**Demo Highlights:**
- User registration and login flow
- Dashboard navigation with 3D widget interactions
- Browsing and listing rental items
- Posting and accepting microtasks
- Trust score system demonstration

### Live Demo
**URL:** 

**Test Credentials:**
- Name: Demo User
- Email: demo@college.edu

---

## Future Enhancements

### Planned Features
1. **Image Upload** - Allow users to upload images for rental items
2. **Search & Filters** - Advanced search with category and price filters
3. **Chat System** - Direct messaging between users
4. **Payment Integration** - Secure payment gateway (Razorpay/Stripe)
5. **Reviews & Ratings** - User reviews for completed transactions
6. **Email Notifications** - Alerts for task assignments and completions
7. **Mobile App** - Native iOS and Android applications
8. **Admin Panel** - Moderation tools for campus administrators
9. **Location-based Search** - Find items and tasks near you
10. **Analytics Dashboard** - User statistics and platform metrics

---

## Security Features

- **Session Management** - Secure Flask sessions with secret key
- **SQL Injection Prevention** - Parameterized queries with SQLite
- **Input Validation** - Form data validation on backend
- **HTTPS Ready** - Secure deployment configurations
- **Trust System** - Reputation-based access control

---

## Known Issues & Limitations

1. **No Password Authentication** - Currently uses name/email only (planned for v2.0)
2. **No Image Upload** - Items listings are text-only (planned enhancement)
3. **Basic Search** - No advanced filtering yet
4. **No Real-time Updates** - Page refresh needed for new data
5. **Single Campus** - No multi-campus support yet

---

## Contributing

We welcome contributions! Here's how you can help:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/AmazingFeature`)
3. **Commit your changes** (`git commit -m 'Add some AmazingFeature'`)
4. **Push to the branch** (`git push origin feature/AmazingFeature`)
5. **Open a Pull Request**

### Contribution Guidelines
- Follow PEP 8 style guide for Python code
- Write descriptive commit messages
- Test thoroughly before submitting PR
- Update documentation for new features

---

## Testing

### Manual Testing Checklist

**Authentication:**
- [ ] User can register with name and email
- [ ] Existing users can login
- [ ] Session persists across pages
- [ ] Logout clears session properly

**Rental Items:**
- [ ] View all items successfully
- [ ] List new item with all fields
- [ ] Item appears in browse page immediately
- [ ] Form validation works correctly

**Micro Tasks:**
- [ ] Browse all posted tasks
- [ ] Post new task successfully
- [ ] Accept task updates status
- [ ] Complete task increases trust score
- [ ] Status changes reflect correctly

**Trust System:**
- [ ] New users start with 100 points
- [ ] Completing task adds +5 points
- [ ] Trust score displays on dashboard

---

## Team Contributions

- **[Member 1]:** Backend development, database design, Flask routes, authentication system
- **[Member 2]:** Frontend development, UI/UX design, premium theme implementation, documentation

---

## Acknowledgments

- **Flask Documentation** - Comprehensive web framework guide
- **SQLite** - Lightweight database solution
- **Bootstrap Icons** - Icon library
- **Font Awesome** - Additional icons
- **TinkerHub** - Platform and support for the hackathon

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

**MIT License Overview:**
- ✅ Commercial use allowed
- ✅ Modification allowed
- ✅ Distribution allowed
- ✅ Private use allowed
- ❗ Liability and warranty not included

---

## Contact & Support

**Project Repository:** https://github.com/alfiagit27/campus-rental



**Issues & Bug Reports:** [GitHub Issues](https://github.com/alfiagit27/campus-rental/issues)

**For queries:** alfiasset@gmail.com

---

## Project Statistics

- **Total Routes:** 10
- **Database Tables:** 3
- **Templates:** 9
- **Lines of Code:** ~250 (Python)
- **Development Time:** [Your duration]
- **Contributors:** 2

---

<p align="center">
  Made with ❤️ at TinkerHub
</p>

<p align="center">
  <strong>CampusConnect - Connecting Students, Building Community</strong>
</p>

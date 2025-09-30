# Expense Tracker Frontend

A modern React application for tracking daily expenses with a beautiful, responsive UI.

## Features

- 🎨 Modern, responsive design with Tailwind CSS
- 🔐 Authentication (Login/Register)
- 📊 Interactive dashboard with charts
- 💰 Expense management (CRUD)
- 📱 Mobile-first responsive design
- 🚀 Fast performance with Vite
- 📈 Data visualization with Recharts
- 🎯 Form validation with React Hook Form
- 🔄 Real-time data with React Query

## Tech Stack

- **Framework**: React 18
- **Build Tool**: Vite
- **Styling**: Tailwind CSS
- **Routing**: React Router DOM
- **State Management**: React Query
- **Forms**: React Hook Form
- **Charts**: Recharts
- **Icons**: Lucide React
- **HTTP Client**: Axios

## Quick Start

### Prerequisites

- Node.js (v16 or higher)
- npm or yarn

### Installation

1. **Install dependencies**:
   ```bash
   npm install
   ```

2. **Environment setup**:
   ```bash
   cp config.env .env
   # Edit .env with your API URL
   ```

3. **Start development server**:
   ```bash
   npm run dev
   ```

4. **Build for production**:
   ```bash
   npm run build
   ```

### Environment Variables

Create a `.env` file with:

```env
VITE_API_URL=http://localhost:5000/api
```

## Project Structure

```
frontend/
├── src/
│   ├── components/     # Reusable components
│   ├── pages/          # Page components
│   ├── context/        # React context
│   ├── hooks/          # Custom hooks
│   ├── utils/          # Utility functions
│   ├── App.jsx         # Main app component
│   └── main.jsx        # Entry point
├── public/             # Static assets
└── index.html          # HTML template
```

## Pages

- **Login** - User authentication
- **Register** - User registration
- **Dashboard** - Overview with charts and stats
- **Expenses** - List and manage expenses
- **Add Expense** - Create new expense
- **Profile** - User profile management

## Components

- **Layout** - Main layout with sidebar navigation
- **LoadingSpinner** - Loading indicator
- **Charts** - Data visualization components

## Deployment

### Ubuntu Server Setup

1. **Install Node.js**:
   ```bash
   curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
   sudo apt-get install -y nodejs
   ```

2. **Install Nginx**:
   ```bash
   sudo apt update
   sudo apt install nginx
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

3. **Build and deploy**:
   ```bash
   # Build the application
   npm run build
   
   # Copy dist folder to nginx directory
   sudo cp -r dist/* /var/www/html/
   ```

### Nginx Configuration

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /var/www/html;
    index index.html;
    
    location / {
        try_files $uri $uri/ /index.html;
    }
    
    location /api {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_cache_bypass $http_upgrade;
    }
}
```

### PM2 for Process Management

```bash
# Install PM2 globally
sudo npm install -g pm2

# Create ecosystem file
cat > ecosystem.config.js << EOF
module.exports = {
  apps: [{
    name: 'expense-tracker-frontend',
    script: 'npm',
    args: 'run preview',
    cwd: '/path/to/your/frontend',
    env: {
      NODE_ENV: 'production',
      PORT: 3000
    }
  }]
}
EOF

# Start with PM2
pm2 start ecosystem.config.js
pm2 save
pm2 startup
```

## Development

### Scripts
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint

### Key Features

#### Authentication
- JWT-based authentication
- Protected routes
- Automatic token refresh
- Secure logout

#### Dashboard
- Expense statistics
- Category breakdown (pie chart)
- Monthly trends (bar chart)
- Recent transactions

#### Expense Management
- Add/edit/delete expenses
- Category filtering
- Search functionality
- Pagination

#### Responsive Design
- Mobile-first approach
- Touch-friendly interface
- Adaptive layouts
- Modern UI components

## Styling

The application uses Tailwind CSS with custom components:

- **Colors**: Primary blue theme with secondary grays
- **Typography**: Inter font family
- **Components**: Custom button, input, and card styles
- **Animations**: Smooth transitions and loading states
- **Icons**: Lucide React icon library

## Performance

- **Code Splitting**: Automatic route-based splitting
- **Lazy Loading**: Components loaded on demand
- **Optimized Build**: Vite's fast build system
- **Caching**: React Query for data caching
- **Bundle Size**: Optimized with tree shaking

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

MIT License
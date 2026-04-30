<!DOCTYPE html>
<html>
<head>
  <base target="_top">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    :root {
      --primary-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      --primary-color: #667eea;
      --border-color: #e5e7eb;
      --text-gray: #6b7280;
      --bg-gray: #f9fafb;
      --shadow-sm: 0 2px 10px rgba(0,0,0,0.08);
      --shadow-md: 0 4px 15px rgba(102, 126, 234, 0.2);
      --shadow-lg: 0 20px 60px rgba(102, 126, 234, 0.3);
      --radius: 6px;
      --radius-lg: 10px;
      --transition: all 0.3s ease;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #fff;
      overflow-x: hidden;
    }

    /* Login Page Styles */
    .login-container {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      background: var(--primary-gradient);
      padding: 20px;
    }

    .login-card {
      background: white;
      border-radius: 20px;
      padding: 50px 40px;
      box-shadow: var(--shadow-lg);
      max-width: 450px;
      width: 100%;
      animation: fadeInUp 0.5s ease;
    }

    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(30px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .login-header {
      text-align: center;
      margin-bottom: 40px;
    }

    .login-header h1 {
      font-size: 36px;
      background: var(--primary-gradient);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 10px;
    }

    .login-header p {
      color: var(--text-gray);
      font-size: 16px;
    }

    .form-group {
      margin-bottom: 25px;
    }

    .form-group label {
      display: block;
      margin-bottom: 10px;
      font-weight: 500;
      color: #374151;
      font-size: 14px;
    }

    .form-group input, .form-group select, .form-group textarea {
      width: 100%;
      padding: 14px;
      border: 2px solid var(--border-color);
      border-radius: var(--radius);
      font-size: 15px;
      transition: var(--transition);
      font-family: inherit;
    }

    .form-group textarea {
      resize: vertical;
      min-height: 100px;
    }

    .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
      outline: none;
      border-color: var(--primary-color);
      box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
    }

    .btn-primary {
      width: 100%;
      padding: 14px;
      background: var(--primary-gradient);
      color: white;
      border: none;
      border-radius: var(--radius);
      font-size: 16px;
      font-weight: 600;
      cursor: pointer;
      transition: var(--transition);
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
    }

    .btn-primary:hover {
      transform: translateY(-2px);
      box-shadow: var(--shadow-md);
    }

    .btn-primary:active {
      transform: translateY(0);
    }

    .btn-primary:disabled {
      opacity: 0.6;
      cursor: not-allowed;
      transform: none;
    }

    .btn-primary:active {
      transform: translateY(0);
    }

    .error-message {
      background-color: #fee2e2;
      color: #991b1b;
      padding: 12px;
      border-radius: var(--radius);
      margin-bottom: 20px;
      font-size: 14px;
      display: none;
      align-items: center;
      gap: 10px;
    }

    .error-message.show {
      display: flex;
    }

    /* App Container */
    .app-container {
      display: flex;
      height: 100vh;
      background: #fff;
    }

    #sidebar {
      width: 260px;
      background: var(--primary-gradient);
      color: white;
      display: flex;
      flex-direction: column;
      transition: var(--transition);
      position: relative;
      z-index: 100;
    }

    .sidebar-header {
      padding: 25px;
      font-size: 24px;
      font-weight: bold;
      text-align: center;
      border-bottom: 1px solid rgba(255,255,255,0.1);
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
    }

    .menu-items {
      flex: 1;
      padding: 20px 0;
      overflow-y: auto;
    }

    .menu-item {
      padding: 16px 30px;
      cursor: pointer;
      transition: var(--transition);
      display: flex;
      align-items: center;
      gap: 15px;
      font-size: 15px;
      color: rgba(255,255,255,0.9);
      position: relative;
    }

    .menu-item i {
      font-size: 18px;
      min-width: 20px;
    }

    .menu-item:hover, .menu-item.active {
      background: rgba(255,255,255,0.15);
      color: white;
    }

    .menu-item.active::before {
      content: '';
      position: absolute;
      left: 0;
      top: 0;
      bottom: 0;
      width: 4px;
      background: white;
    }

    .sidebar-footer {
      padding: 20px;
      border-top: 1px solid rgba(255,255,255,0.1);
    }

    .logout-btn {
      width: 100%;
      padding: 12px;
      background: rgba(255,255,255,0.2);
      color: white;
      border: none;
      border-radius: var(--radius);
      cursor: pointer;
      font-size: 15px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      transition: var(--transition);
    }
    /* Collapsible Sidebar Styles */
    #sidebar {
      width: 260px;
      background: var(--primary-gradient);
      color: white;
      display: flex;
      flex-direction: column;
      transition: width 0.3s ease, padding 0.3s ease;
      position: relative;
      z-index: 100;
    }
    
    #sidebar.collapsed {
      width: 70px;
    }
    
    #sidebar.collapsed .menu-item span,
    #sidebar.collapsed .sidebar-header span,
    #sidebar.collapsed .powered-by {
      opacity: 0;
      width: 0;
      overflow: hidden;
      transition: opacity 0.2s ease;
    }
    
    #sidebar.collapsed .logout-btn span {
      display: none;
    }
    
    #sidebar.collapsed .menu-item {
      justify-content: center;
      padding: 16px 10px;
    }
    
    #sidebar.collapsed .sidebar-header {
      padding: 25px 10px;
      justify-content: center;
    }
    
    .menu-item span {
      transition: opacity 0.3s ease;
      white-space: nowrap;
    }
    
    .hamburger-toggle {
      position: absolute;
      top: 20px;
      right: 15px;
      cursor: pointer;
      font-size: 20px;
      z-index: 101;
      color: white;
      transition: transform 0.3s ease;
    }
    
    #sidebar.collapsed .hamburger-toggle {
      right: auto;
      left: 50%;
      transform: translateX(-50%);
    }

    .logout-btn:hover {
      background: rgba(255,255,255,0.3);
    }

    .powered-by {
      text-align: center;
      margin-top: 15px;
      font-size: 12px;
      color: rgba(255,255,255,0.7);
    }

    #main-content {
      flex: 1;
      overflow-y: auto;
      background: #f5f5f7;
    }

    /* Welcome Section */
    .welcome-container {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    .welcome-card {
      background: white;
      border-radius: 20px;
      padding: 60px 40px;
      box-shadow: var(--shadow-lg);
      text-align: center;
      max-width: 600px;
      animation: fadeInUp 0.5s ease;
    }

    .welcome-card h1 {
      font-size: 48px;
      background: var(--primary-gradient);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 20px;
    }

    .welcome-card .username {
      font-size: 24px;
      color: #374151;
      margin-bottom: 20px;
      font-weight: 600;
    }

    .welcome-card p {
      color: var(--text-gray);
      font-size: 18px;
      line-height: 1.6;
    }

    .welcome-card strong {
      color: var(--primary-color);
    }

    /* Data Sections */
    .data-section {
      display: none;
      padding: 30px;
      animation: fadeInUp 0.5s ease;
    }

    .section-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 30px;
      flex-wrap: wrap;
      gap: 15px;
    }

    .section-header h2 {
      font-size: 28px;
      color: #374151;
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .section-header h2 i {
      background: var(--primary-gradient);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .section-header .btn-primary {
      width: auto;
      padding: 12px 24px;
      font-size: 15px;
    }

    .search-box {
      margin-bottom: 25px;
    }

    .search-box input {
      width: 100%;
      max-width: 400px;
      padding: 12px 20px;
      border: 2px solid var(--border-color);
      border-radius: var(--radius-lg);
      font-size: 15px;
      transition: var(--transition);
    }

    .search-box input:focus {
      outline: none;
      border-color: var(--primary-color);
      box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
    }


    /* TABLE STYLES (for Customers and Inventory) */


    .data-table-container {
      background: white;
      border-radius: var(--radius-lg);
      box-shadow: var(--shadow-sm);
      overflow: hidden;
    }

    .data-table {
      width: 100%;
      border-collapse: collapse;
      font-size: 14px;
    }

    .data-table thead {
      background: linear-gradient(135deg, #4a90e2 0%, #764ba2 100%);
    }

    .data-table thead th {
      padding: 16px;
      text-align: left;
      font-weight: 600;
      color: white;
      text-transform: uppercase;
      font-size: 13px;
      letter-spacing: 0.5px;
    }

    .data-table tbody tr {
      border-bottom: 1px solid var(--border-color);
      transition: background-color 0.2s ease;
    }

    .data-table tbody tr:hover {
      background-color: #f9fafb;
    }

    .data-table tbody tr:last-child {
      border-bottom: none;
    }

    .data-table tbody td {
      padding: 14px 16px;
      color: #374151;
    }

    .badge {
      display: inline-block;
      padding: 4px 12px;
      border-radius: 12px;
      font-size: 12px;
      font-weight: 600;
    }

    .badge-primary {
      background: #667eea;
      color: white;
    }

    .badge-success {
      background: #10b981;
      color: white;
    }

    .badge-info {
      background: #3b82f6;
      color: white;
    }

    .badge-warning {
      background: #f59e0b;
      color: white;
    }

    .badge-secondary {
      background: #e0e7ff;
      color: #667eea;
    }

    .btn-edit-table {
      background: #14b8a6;
      color: white;
      border: none;
      padding: 8px 16px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: var(--transition);
    }

    .btn-edit-table:hover {
      background: #0d9488;
      transform: translateY(-1px);
    }

    .btn-delete-table {
      background: #ef4444;
      color: white;
      border: none;
      padding: 8px 16px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: var(--transition);
      margin-left: 8px;
    }

    .btn-delete-table:hover {
      background: #dc2626;
      transform: translateY(-1px);
    }

    .table-actions {
      display: flex;
      gap: 8px;
    }

    /* Empty State */
    .empty-state {
      text-align: center;
      padding: 80px 20px;
      background: white;
      border-radius: var(--radius-lg);
      box-shadow: var(--shadow-sm);
    }

    .empty-state i {
      font-size: 80px;
      background: var(--primary-gradient);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 20px;
    }

    .empty-state h3 {
      font-size: 24px;
      color: #374151;
      margin-bottom: 10px;
    }

    .empty-state p {
      color: var(--text-gray);
      font-size: 16px;
      margin-bottom: 30px;
    }

    /* PRICE LIST CARDS */
    .data-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
      gap: 20px;
    }

    .data-card {
      background: white;
      border-radius: var(--radius-lg);
      padding: 25px;
      box-shadow: var(--shadow-sm);
      transition: var(--transition);
      border: 1px solid var(--border-color);
    }

    .data-card:hover {
      transform: translateY(-4px);
      box-shadow: var(--shadow-md);
    }

    .data-card h3 {
      font-size: 18px;
      color: #374151;
      margin-bottom: 20px;
      display: flex;
      align-items: center;
      gap: 10px;
      padding-bottom: 15px;
      border-bottom: 2px solid var(--bg-gray);
    }

    .data-card h3 i {
      color: var(--primary-color);
    }

    .data-row {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      padding: 10px 0;
      border-bottom: 1px solid var(--bg-gray);
    }

    .data-row:last-of-type {
      border-bottom: none;
    }

    .data-label {
      color: var(--text-gray);
      font-size: 14px;
      font-weight: 500;
    }

    .data-value {
      color: #374151;
      font-size: 14px;
      text-align: right;
      max-width: 60%;
      word-wrap: break-word;
    }

    .card-actions {
      display: flex;
      gap: 10px;
      margin-top: 20px;
      padding-top: 15px;
      border-top: 2px solid var(--bg-gray);
    }

    .btn-edit, .btn-delete {
      flex: 1;
      padding: 10px;
      border: none;
      border-radius: var(--radius);
      font-size: 14px;
      font-weight: 500;
      cursor: pointer;
      transition: var(--transition);
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }

    .btn-edit {
      background: #667eea;
      color: white;
    }

    .btn-edit:hover {
      background: #5568d3;
      transform: translateY(-2px);
    }

    .btn-delete {
      background: #ef4444;
      color: white;
    }

    .btn-delete:hover {
      background: #dc2626;
      transform: translateY(-2px);
    }

    /* Modals */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      z-index: 1000;
      align-items: center;
      justify-content: center;
      padding: 20px;
      animation: fadeIn 0.3s ease;
    }

    .modal.active {
      display: flex;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    .modal-content {
      background: white;
      border-radius: var(--radius-lg);
      width: 100%;
      max-width: 600px;
      max-height: 90vh;
      overflow-y: auto;
      box-shadow: var(--shadow-lg);
      animation: slideUp 0.3s ease;
    }

    @keyframes slideUp {
      from { transform: translateY(50px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    .modal-header {
      padding: 25px 30px;
      border-bottom: 2px solid var(--bg-gray);
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: var(--primary-gradient);
      color: white;
      border-radius: var(--radius-lg) var(--radius-lg) 0 0;
    }

    .modal-header h2 {
      font-size: 22px;
      display: flex;
      align-items: center;
      gap: 10px;
      margin: 0;
      color: white;
    }

    .modal-close {
      background: rgba(255,255,255,0.2);
      border: none;
      color: white;
      font-size: 24px;
      cursor: pointer;
      width: 36px;
      height: 36px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: var(--transition);
    }

    .modal-close:hover {
      background: rgba(255,255,255,0.3);
      transform: rotate(90deg);
    }

    .modal-body {
      padding: 30px;
    }

    /* Margin Editable */
    .editable-margin {
      background: #fef3c7;
      padding: 4px 8px;
      border-radius: 4px;
      cursor: pointer;
      font-weight: 600;
      transition: var(--transition);
    }

    .editable-margin:hover {
      background: #fde68a;
    }

    /* Mode Selection Buttons */
    .btn-mode {
      flex: 1;
      padding: 12px 20px;
      border: 2px solid var(--border-color);
      background: white;
      color: #374151;
      border-radius: var(--radius);
      font-size: 14px;
      font-weight: 500;
      cursor: pointer;
      transition: var(--transition);
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }

    .btn-mode:hover {
      border-color: var(--primary-color);
      background: #f0f4ff;
    }

    .btn-mode.active {
      background: var(--primary-gradient);
      color: white;
      border-color: var(--primary-color);
    }

    /* Search Results */
    .search-result-item {
      padding: 12px;
      border-bottom: 1px solid var(--border-color);
      cursor: pointer;
      transition: var(--transition);
    }

    .search-result-item:last-child {
      border-bottom: none;
    }

    .search-result-item:hover {
      background: #f9fafb;
    }

    .search-result-item strong {
      color: #374151;
      display: block;
      margin-bottom: 4px;
    }

    .search-result-item small {
      color: var(--text-gray);
      font-size: 12px;
    }

    .readonly-field {
      background-color: #f3f4f6;
      cursor: not-allowed;
    }

    /* Mobile Styles */
    #mobile-toggle-btn {
      display: none;
      position: fixed;
      top: 20px;
      left: 20px;
      z-index: 101;
      background: var(--primary-gradient);
      color: white;
      border: none;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      font-size: 20px;
      cursor: pointer;
      box-shadow: var(--shadow-md);
    }

    @media (max-width: 768px) {
      #mobile-toggle-btn {
        display: flex;
        align-items: center;
        justify-content: center;
      }

      #sidebar {
        position: fixed;
        left: -260px;
        top: 0;
        height: 100vh;
        z-index: 102;
      }

      #sidebar.show {
        left: 0;
      }

      #main-content {
        margin-left: 0;
      }

      .data-grid {
        grid-template-columns: 1fr;
      }

      .section-header {
        flex-direction: column;
        align-items: flex-start;
      }

      .section-header .btn-primary {
        width: 100%;
      }

      .data-table-container {
        overflow-x: auto;
      }

      .data-table {
        min-width: 1000px;
      }
    }
  </style>
</head>
<body>

  <!-- Login Page -->
  <div id="loginPage" class="login-container">
    <div class="login-card">
      <div class="login-header">
        <h1>ALCOBINA</h1>
        <p>Welcome back! Please login to continue</p>
      </div>
      
      <div id="loginError" class="error-message">
        <i class="fas fa-exclamation-circle"></i>
        <span id="loginErrorText"></span>
      </div>

      <form id="loginForm">
        <div class="form-group">
          <label><i class="fas fa-envelope"></i> Email Address</label>
          <input type="email" id="loginEmail" required placeholder="Enter your email">
        </div>

        <div class="form-group">
          <label><i class="fas fa-lock"></i> Password</label>
          <input type="password" id="loginPassword" required placeholder="Enter your password">
        </div>

        <button type="submit" class="btn-primary" id="loginBtn">
          <i class="fas fa-sign-in-alt"></i> <span>Login</span>
        </button>
      </form>
    </div>
  </div>

  <!-- App Container -->
  <div id="appContainer" class="app-container" style="display:none;">
    <!-- Mobile Toggle Button -->
    <button id="mobile-toggle-btn" onclick="toggleSidebar()">
      <i class="fas fa-bars"></i>
    </button>

    <!-- Sidebar -->
    <div id="sidebar">
      <div class="sidebar-header" onclick="toggleSidebar()">
        <i class="fas fa-bars"></i> ALCOBINA
      </div>
      <div class="menu-items">
        <div class="menu-item active" onclick="showWelcome()">
          <i class="fas fa-home"></i><span>Home</span>
        </div>
        <div class="menu-item" onclick="showInventory()">
          <i class="fas fa-boxes"></i><span>Inventory History</span>
        </div>
        <div class="menu-item" onclick="showPOS()">
          <i class="fas fa-cash-register"></i><span>POS</span>
        </div>
        <div class="menu-item" onclick="showPriceList()">
          <i class="fas fa-tags"></i><span>Price List</span>
        </div>
        <div class="menu-item" onclick="showComingSoon('Sales Dashboard', 'chart-line')">
          <i class="fas fa-chart-line"></i><span>Sales Dashboard</span>
        </div>
        <div class="menu-item" onclick="showCustomers()">
          <i class="fas fa-users"></i><span>Customers</span>
        </div>
        <div class="menu-item" onclick="showItemLookup()">
          <i class="fas fa-search"></i><span>Item Lookup</span>
        </div>
        <div class="menu-item" onclick="showComingSoon('Collections', 'money-bill-wave')">
          <i class="fas fa-money-bill-wave"></i><span>Collections</span>
        </div>
        <div class="menu-item" onclick="showComingSoon('Purchase History', 'shopping-cart')">
          <i class="fas fa-shopping-cart"></i><span>Purchase History</span>
        </div>
      </div>
      <div class="sidebar-footer">
        <button class="logout-btn" onclick="logout()">
          <i class="fas fa-sign-out-alt"></i> Logout
        </button>
        <div class="powered-by">Powered by <strong>ALCOBINA</strong></div>
      </div>
    </div>

    <!-- Main Content -->
    <div id="main-content">
      <!-- Welcome Screen -->
      <div id="welcome-section" class="welcome-container" style="display: flex;">
        <div class="welcome-card">
          <h1>👋 Welcome</h1>
          <div class="username" id="welcome-username">User</div>
          <p>To the ALCOBINA Portal<br>
          <strong id="business-name-display">Your Business</strong><br>
          Client ID: <strong id="client-id-display">Loading...</strong><br>
          User UID: <strong id="user-uid-display">Loading...</strong></p>
          <p style="margin-top: 20px;">Please select an option from the menu to get started</p>
        </div>
      </div>

      <!-- Inventory History Section -->
      <div id="inventory-section" class="data-section">
        <div class="section-header">
          <h2><i class="fas fa-boxes"></i> Inventory History</h2>
          <button class="btn-primary" onclick="openAddInventoryModal()">
            <i class="fas fa-plus"></i> Add Inventory Entry
          </button>
        </div>

        <div class="search-box">
          <input type="text" id="inventorySearchInput" placeholder="🔍 Search by item name, barcode, category, vendor..." onkeyup="filterInventory()">
        </div>

        <div id="inventoryContainer"></div>
      </div>

      <!-- Price List Section -->
      <div id="price-list-section" class="data-section">
        <div class="section-header">
          <h2><i class="fas fa-tags"></i> Price List</h2>
          <div style="display: flex; gap: 10px;">
            <button class="btn-primary" id="downloadSelectedPDF" onclick="downloadSelectedPricePDF()" disabled>
              <i class="fas fa-download"></i> Download PDF
            </button>
            <button class="btn-primary" id="emailSelectedPDF" onclick="emailSelectedPricePDF()" disabled>
              <i class="fas fa-envelope"></i> Email PDF
            </button>
            <button class="btn-primary" onclick="downloadAllPricesPDF()">
              <i class="fas fa-file-pdf"></i> Download All
            </button>
            <button class="btn-primary" onclick="syncPriceListFromInventory()">
              <i class="fas fa-sync"></i> Sync Costs
            </button>
          </div>
        </div>

        <div class="search-box">
          <input type="text" id="priceSearchInput" placeholder="🔍 Search by item name, number, or description..." onkeyup="filterPriceList()">
        </div>

        <div id="priceListContainer"></div>
      </div>

      <!-- Customers Section -->
      <div id="customers-section" class="data-section">
        <div class="section-header">
          <h2><i class="fas fa-users"></i> Customers</h2>
          <div style="display: flex; gap: 10px;">
            <button class="btn-secondary" onclick="showBulkUploadInstructions()">
              <i class="fas fa-file-excel"></i> Bulk Upload
            </button>
            <button class="btn-primary" onclick="openAddCustomerModal()">
              <i class="fas fa-user-plus"></i> Add Customer
            </button>
          </div>
        </div>

        <div class="search-box">
          <input type="text" id="customerSearchInput" placeholder="🔍 Search customers..." onkeyup="filterCustomers()">
        </div>

        <div id="customersContainer"></div>
      </div>

      <!-- Item Lookup Section -->
      <div id="item-lookup-section" class="data-section" style="display:none;">
        <div class="section-header">
          <h2><i class="fas fa-search"></i> Item Lookup</h2>
        </div>

        <div class="search-box">
          <input type="text" id="itemLookupSearchInput" placeholder="🔍 Search by item name, number, barcode, or description..." onkeyup="filterItemLookup()">
        </div>

        <div id="itemLookupContainer"></div>
      </div>
      <!-- POS Section -->
      <div id="pos-section" class="data-section" style="display:none;">
        <div class="section-header">
          <h2><i class="fas fa-cash-register"></i> Point of Sale</h2>
          <div style="display: flex; gap: 10px;">
            <button class="btn-secondary" onclick="openSearchTransactions()">
              <i class="fas fa-search"></i> Search Transactions
            </button>
            <button class="btn-primary" onclick="clearPOS()">
              <i class="fas fa-plus"></i> New Sale
            </button>
          </div>
        </div>

        <div style="display: grid; grid-template-columns: 1fr 450px; gap: 20px; margin-top: 20px;">
          
          <!-- LEFT: Sale Builder -->
          <div style="background: white; border-radius: 12px; padding: 25px; box-shadow: var(--shadow);">
            
            <!-- Customer & Rep Selection -->
            <div style="display: grid; grid-template-columns: 2fr 1fr; gap: 15px; margin-bottom: 20px;">
              <div class="form-group" style="margin: 0;">
                <label><i class="fas fa-user"></i> Customer *</label>
                <select id="posCustomer" onchange="handleCustomerChange()" required>
                  <option value="">Select Customer...</option>
                </select>
                <div id="customerInfo" style="display: none; margin-top: 8px; padding: 10px; background: #e3f2fd; border-radius: 5px; font-size: 13px;">
                  <div><strong>Email:</strong> <span id="customerEmail">-</span></div>
                  <div id="creditLimitInfo" style="display: none;">
                    <strong>Credit Limit:</strong> $<span id="customerCreditLimit">0</span>
                    <span id="creditWarning" style="color: #f44336; font-weight: 600; display: none;"></span>
                  </div>
                </div>
              </div>
              
              <div class="form-group" style="margin: 0;">
                <label><i class="fas fa-id-badge"></i> Rep ID</label>
                <input type="number" id="posRepId" value="1" min="1" readonly style="background: #f5f5f5;">
              </div>
            </div>

            <!-- Transaction Type & Payment Terms -->
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 20px;">
              <div class="form-group" style="margin: 0;">
                <label><i class="fas fa-dollar-sign"></i> Transaction Type</label>
                <select id="posTransactionType" onchange="handleTransactionTypeChange()">
                  <option value="Cash">Cash</option>
                  <option value="Credit">Credit</option>
                </select>
              </div>
              
              <div class="form-group" style="margin: 0;">
                <label><i class="fas fa-calendar"></i> Payment Terms (Days)</label>
                <select id="posPaymentTerms" disabled>
                  <option value="0">0 (Immediate)</option>
                  <option value="14">14 Days</option>
                  <option value="30">30 Days</option>
                </select>
              </div>
            </div>

            <!-- Item Selection -->
            <div style="background: #f9f9f9; border-radius: 8px; padding: 15px; margin-bottom: 20px;">
              <h3 style="margin: 0 0 15px 0; font-size: 16px;"><i class="fas fa-shopping-cart"></i> Add Items</h3>
              
              <div style="display: grid; grid-template-columns: 2fr 1fr 1fr 100px; gap: 10px; align-items: end;">
                <div class="form-group" style="margin: 0;">
                  <label>Item</label>
                  <select id="posItemSelect" onchange="handleItemSelect()">
                    <option value="">Select item...</option>
                  </select>
                  <small id="itemStock" style="color: #666; margin-top: 5px; display: none;">
                    Stock: <span id="itemStockQty">0</span> available
                  </small>
                </div>
                
                <div class="form-group" style="margin: 0;">
                  <label>Quantity</label>
                  <input type="number" id="posQuantity" min="1" value="1">
                </div>
                
                <div class="form-group" style="margin: 0;">
                  <label>Discount %</label>
                  <input type="number" id="posDiscount" min="0" max="100" value="0" step="0.01">
                </div>
                
                <button class="btn-primary" onclick="addItemToSale()" style="height: 42px;">
                  <i class="fas fa-plus"></i> Add
                </button>
              </div>
            </div>

            <!-- Cart Items -->
            <div style="margin-bottom: 20px;">
              <h3 style="margin: 0 0 10px 0; font-size: 16px;"><i class="fas fa-list"></i> Cart Items</h3>
              <div id="posCartItems" style="max-height: 300px; overflow-y: auto;">
                <div style="text-align: center; padding: 40px; color: #999;">
                  <i class="fas fa-shopping-cart" style="font-size: 48px; margin-bottom: 10px;"></i>
                  <p>No items added yet</p>
                </div>
              </div>
            </div>


            <!-- Pre-Sale Actions -->
            <div id="preSaleActions" style="display: flex; gap: 10px; margin: 20px 0; flex-wrap: wrap;">
              <button onclick="sendQuote()" class="btn-secondary" style="flex: 1; min-width: 140px;">
                <i class="fas fa-file-invoice"></i> Send Quote
              </button>
              <button onclick="generatePDFReceipt()" class="btn-secondary" style="flex: 1; min-width: 140px;">
                <i class="fas fa-file-pdf"></i> PDF (COPY)
              </button>
              <button onclick="emailReceiptCopy()" class="btn-secondary" style="flex: 1; min-width: 140px;">
                <i class="fas fa-envelope"></i> Email (COPY)
              </button>
              <button onclick="printReceipt()" class="btn-secondary" style="flex: 1; min-width: 140px;">
                <i class="fas fa-print"></i> Print
              </button>
            </div>
            
            <!-- Action Buttons -->
            <div style="display: flex; gap: 10px; margin-top: 20px;">
              <button class="btn-secondary" onclick="voidAllItems()" style="flex: 1;">
                <i class="fas fa-trash"></i> Void All
              </button>
              <button class="btn-primary" onclick="submitSale()" style="flex: 2;">
                <i class="fas fa-check-circle"></i> Complete Sale
              </button>
            </div>
          </div>

          <!-- RIGHT: Receipt Preview -->
          <div>
            <div style="background: white; border-radius: 12px; padding: 25px; box-shadow: var(--shadow); position: sticky; top: 20px;">
              <h3 style="text-align: center; margin: 0 0 20px 0; font-size: 18px; color: var(--primary-color);">
                <i class="fas fa-receipt"></i> Receipt Preview
              </h3>
              
              <div id="receiptPreview" style="font-family: 'Courier New', monospace; font-size: 12px; line-height: 1.6;">
                <!-- Receipt will be generated here -->
                <div style="text-align: center; color: #999; padding: 60px 20px;">
                  <i class="fas fa-receipt" style="font-size: 48px; margin-bottom: 10px;"></i>
                  <p>Add items to see receipt</p>
                </div>
              </div>

              <!-- Email & PDF Buttons -->
              <div id="receiptActions" style="display: none; margin-top: 20px; padding-top: 20px; border-top: 2px dashed #ddd;">
                <div style="display: flex; gap: 10px;">
                  <button class="btn-secondary" onclick="emailReceipt()" style="flex: 1;">
                    <i class="fas fa-envelope"></i> Email
                  </button>
                  <button class="btn-primary" onclick="downloadReceiptPDF()" style="flex: 1;">
                    <i class="fas fa-download"></i> PDF
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Coming Soon Screen -->
      <div id="coming-soon-section" style="display:none; text-align:center; padding:60px 20px;">
        <div style="background:white; border-radius:20px; padding:60px 40px; box-shadow:var(--shadow-lg); max-width:600px; margin:0 auto;">
          <div style="font-size:80px; margin-bottom:20px;">
            <i id="coming-soon-icon" class="fas fa-rocket" style="background:var(--primary-gradient); -webkit-background-clip:text; -webkit-text-fill-color:transparent;"></i>
          </div>
          <h2 id="coming-soon-title" style="font-size:36px; margin-bottom:15px; background:var(--primary-gradient); -webkit-background-clip:text; -webkit-text-fill-color:transparent;">Coming Soon</h2>
          <p id="coming-soon-text" style="color:var(--text-gray); font-size:18px;">We're working hard to bring you this feature. Stay tuned!</p>
        </div>
      </div>
    </div>
  </div>

  <!-- Add/Edit Inventory Modal -->
  <div id="inventoryModal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2 id="inventoryModalTitle"><i class="fas fa-box"></i> Add Inventory Entry</h2>
        <button class="modal-close" onclick="closeInventoryModal()"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body">
        <!-- Mode Selection -->
        <div class="form-group" id="inventoryModeSelection">
          <label style="font-weight: 600; font-size: 16px; margin-bottom: 15px; display: block;">
            <i class="fas fa-layer-group"></i> Select Mode:
          </label>
          <div style="display: flex; gap: 10px;">
            <button type="button" class="btn-mode active" id="btnNewItem" onclick="setInventoryMode('new')">
              <i class="fas fa-plus-circle"></i> Create New Item
            </button>
            <button type="button" class="btn-mode" id="btnExistingItem" onclick="setInventoryMode('existing')">
              <i class="fas fa-search"></i> Select Existing Item
            </button>
          </div>
        </div>

        <!-- Search Existing Items -->
        <div class="form-group" id="existingItemSearch" style="display: none;">
          <label><i class="fas fa-search"></i> Search Existing Items</label>
          <input type="text" id="inventorySearchBox" placeholder="🔍 Search or view all unique items..." oninput="searchExistingInventory()">
          <div id="searchResults" style="margin-top: 10px; max-height: 200px; overflow-y: auto; border: 1px solid var(--border-color); border-radius: var(--radius); display: none;"></div>
        </div>

        <form id="inventoryForm">
          <input type="hidden" id="inventoryDocId">
          <input type="hidden" id="inventoryMode" value="new">
          
          <div class="form-group">
            <label><i class="fas fa-hashtag"></i> Item Number *</label>
            <input type="text" id="inventoryItemNumber" required placeholder="e.g., IME-001">
          </div>

          <div class="form-group">
            <label><i class="fas fa-box"></i> Item Name *</label>
            <input type="text" id="inventoryItemName" required placeholder="e.g., Busta - 355 ML">
          </div>

          <div class="form-group">
            <label><i class="fas fa-barcode"></i> Barcode *</label>
            <input type="text" id="inventoryBarcode" required placeholder="e.g., 000129100031">
          </div>

          <div class="form-group">
            <label><i class="fas fa-align-left"></i> Description</label>
            <textarea id="inventoryDescription" placeholder="e.g., Pineapple"></textarea>
          </div>

          <div class="form-group">
            <label><i class="fas fa-tag"></i> Category *</label>
            <select id="inventoryCategory" required>
              <option value="">Select Category</option>
              <option value="Beverage">Beverage</option>
              <option value="Food">Food</option>
              <option value="Snacks">Snacks</option>
              <option value="Alcohol">Alcohol</option>
              <option value="Supplies">Supplies</option>
              <option value="Other">Other</option>
            </select>
          </div>

          <div class="form-group">
            <label><i class="fas fa-cubes"></i> Quantity *</label>
            <input type="number" id="inventoryQuantity" required min="0" placeholder="e.g., 50">
          </div>

          <div class="form-group">
            <label><i class="fas fa-dollar-sign"></i> Unit Cost *</label>
            <input type="number" id="inventoryUnitCost" required min="0" step="0.01" placeholder="e.g., 1500">
          </div>

          <div class="form-group">
            <label><i class="fas fa-balance-scale"></i> Unit of Measure *</label>
            <select id="inventoryUnitOfMeasure" required>
              <option value="">Select Unit</option>
              <option value="cs">Case (cs)</option>
              <option value="box">Box</option>
              <option value="bottle">Bottle</option>
              <option value="can">Can</option>
              <option value="unit">Unit</option>
              <option value="pack">Pack</option>
              <option value="liter">Liter</option>
            </select>
          </div>

          <div class="form-group">
            <label><i class="fas fa-truck"></i> Vendor *</label>
            <input type="text" id="inventoryVendor" required placeholder="e.g., Sampars">
          </div>

          <div class="form-group">
            <label><i class="fas fa-calendar"></i> Posting Date *</label>
            <input type="datetime-local" id="inventoryPostingDate" required>
          </div>

          <button type="submit" class="btn-primary">
            <i class="fas fa-save"></i> Save Entry
          </button>
        </form>
      </div>
    </div>
  </div>

  <!-- Add/Edit Price Modal -->
  <div id="priceModal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2 id="priceModalTitle"><i class="fas fa-tag"></i> Add Price Item</h2>
        <button class="modal-close" onclick="closePriceModal()"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body">
        <form id="priceForm">
          <input type="hidden" id="priceDocId">
          
          <div class="form-group">
            <label><i class="fas fa-hashtag"></i> Item Number *</label>
            <input type="text" id="priceItemNumber" required placeholder="e.g., ITEM-002">
          </div>

          <div class="form-group">
            <label><i class="fas fa-box"></i> Item Name *</label>
            <input type="text" id="priceItemName" required placeholder="e.g., Corona Extra 355 ML">
          </div>

          <div class="form-group">
            <label><i class="fas fa-align-left"></i> Description</label>
            <textarea id="priceDescription" placeholder="Optional item description"></textarea>
          </div>

          <div class="form-group">
            <label><i class="fas fa-dollar-sign"></i> Unit Cost *</label>
            <input type="number" id="priceUnitCost" required min="0" step="0.01" placeholder="e.g., 1500">
          </div>

          <div class="form-group">
            <label><i class="fas fa-percentage"></i> Margin (%) *</label>
            <input type="number" id="priceMargin" required min="0" max="100" step="0.1" placeholder="e.g., 12">
          </div>

          <div class="form-group">
            <label><i class="fas fa-balance-scale"></i> Unit of Measure *</label>
            <select id="priceUnitOfMeasure" required>
              <option value="">Select Unit</option>
              <option value="Case">Case</option>
              <option value="Box">Box</option>
              <option value="Bottle">Bottle</option>
              <option value="Can">Can</option>
              <option value="Unit">Unit</option>
              <option value="Pack">Pack</option>
              <option value="Liter">Liter</option>
            </select>
          </div>

          <button type="submit" class="btn-primary">
            <i class="fas fa-save"></i> Save Item
          </button>
        </form>
      </div>
    </div>
  </div>

  <!-- Add/Edit Customer Modal -->
  <div id="customerModal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2 id="customerModalTitle"><i class="fas fa-user"></i> Add Customer</h2>
        <button class="modal-close" onclick="closeCustomerModal()"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body">
        <form id="customerForm">
          <input type="hidden" id="customerDocId">
          <input type="hidden" id="customerNumber">
          
          <div class="form-group">
            <label><i class="fas fa-user"></i> Customer Name *</label>
            <input type="text" id="customerName" required placeholder="e.g., John's Store">
          </div>

          <div class="form-group">
            <label><i class="fas fa-tag"></i> Customer Type</label>
            <select id="customerType">
              <option value="Retail">Retail</option>
              <option value="Wholesale">Wholesale</option>
              <option value="Distributor">Distributor</option>
              <option value="Restaurant">Restaurant</option>
              <option value="Bar">Bar</option>
              <option value="Hotel">Hotel</option>
            </select>
          </div>

          <div class="form-group">
            <label><i class="fas fa-phone"></i> Phone</label>
            <input type="tel" id="customerPhone" placeholder="e.g., (876) 123-4567">
          </div>

          <div class="form-group">
            <label><i class="fas fa-envelope"></i> Email</label>
            <input type="email" id="customerEmail" placeholder="e.g., customer@email.com">
          </div>

          <div class="form-group">
            <label><i class="fas fa-map-marker-alt"></i> Parish</label>
            <select id="customerParish">
              <option value="">Select Parish</option>
              <option value="Kingston">Kingston</option>
              <option value="St. Andrew">St. Andrew</option>
              <option value="St. Catherine">St. Catherine</option>
              <option value="Clarendon">Clarendon</option>
              <option value="Manchester">Manchester</option>
              <option value="St. Elizabeth">St. Elizabeth</option>
              <option value="Westmoreland">Westmoreland</option>
              <option value="Hanover">Hanover</option>
              <option value="St. James">St. James</option>
              <option value="Trelawny">Trelawny</option>
              <option value="St. Ann">St. Ann</option>
              <option value="St. Mary">St. Mary</option>
              <option value="Portland">Portland</option>
              <option value="St. Thomas">St. Thomas</option>
            </select>
          </div>

          <div class="form-group">
            <label><i class="fas fa-map-pin"></i> Address</label>
            <textarea id="customerAddress" placeholder="Full address"></textarea>
          </div>

          <div class="form-group">
            <label><i class="fas fa-credit-card"></i> Credit Limit</label>
            <input type="number" id="customerCreditLimit" min="0" step="0.01" placeholder="e.g., 50000">
          </div>

          <div class="form-group">
            <label><i class="fas fa-sticky-note"></i> Notes</label>
            <textarea id="customerNotes" placeholder="Additional notes about the customer"></textarea>
          </div>

          <button type="submit" class="btn-primary">
            <i class="fas fa-save"></i> Save Customer
          </button>
        </form>
      </div>
    </div>
  </div>


  <!-- Search Transactions Modal -->
  <div id="searchTransactionsModal" class="modal">
    <div class="modal-content" style="max-width: 900px;">
      <div class="modal-header">
        <h2><i class="fas fa-search"></i> Search Transactions</h2>
        <button class="modal-close" onclick="closeSearchTransactions()"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body">
        <!-- Search Box -->
        <div class="search-box" style="margin-bottom: 20px;">
          <input type="text" id="transactionSearchInput" placeholder="🔍 Search by Transaction ID, Customer, Item..." onkeyup="filterTransactions()">
        </div>

        <!-- Results -->
        <div id="transactionResults" style="max-height: 500px; overflow-y: auto;"></div>
      </div>
    </div>
  </div>
  <!-- Bulk Upload Customer Modal -->
  <div id="bulkUploadModal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2><i class="fas fa-file-upload"></i> Bulk Upload Customers</h2>
        <button class="modal-close" onclick="closeBulkUploadModal()"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body">
        <!-- Instructions -->
        <div style="background: #e3f2fd; border-left: 4px solid #2196f3; padding: 15px; margin-bottom: 20px; border-radius: 5px;">
          <h3 style="margin-top: 0; color: #1976d2;"><i class="fas fa-info-circle"></i> Excel Format Required</h3>
          <p style="margin: 10px 0;"><strong>Your Excel file must have these column headers (exact spelling):</strong></p>
          <div style="background: white; padding: 10px; border-radius: 5px; font-family: monospace; margin: 10px 0;">
            customer_name | customer_type | phone | email | parish | address | credit_limit | notes
          </div>
          <p style="margin: 10px 0;"><strong>Example row:</strong></p>
          <div style="background: white; padding: 10px; border-radius: 5px; font-family: monospace; font-size: 12px;">
            John's Store | Retail | (876) 123-4567 | <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="13797c7b7d53767e727a7f3d707c7e">[email&#160;protected]</a> | Kingston | 123 Main St | 50000 | VIP Customer
          </div>
          <p style="margin: 10px 0; color: #666;"><i class="fas fa-lightbulb"></i> <strong>Tips:</strong></p>
          <ul style="margin: 5px 0; padding-left: 20px; color: #666;">
            <li>Customer numbers will be auto-generated (CUST-001, CUST-002, etc.)</li>
            <li>Your client_id (UID-001) will be added automatically</li>
            <li>Duplicate names will be skipped (no duplicates added)</li>
            <li>Save your file as <strong>.csv</strong> or <strong>.xlsx</strong> format</li>
          </ul>
        </div>

        <!-- File Upload -->
        <div class="form-group">
          <label><i class="fas fa-file-excel"></i> Select File (CSV or Excel)</label>
          <input type="file" id="bulkUploadFile" accept=".csv,.xlsx,.xls" style="padding: 10px; border: 2px dashed var(--border-color); border-radius: 8px; width: 100%;">
          <small style="color: #666; margin-top: 5px; display: block;">✅ Accepts: .csv, .xlsx, .xls</small>
        </div>

        <!-- Progress -->
        <div id="uploadProgress" style="display: none; margin: 20px 0;">
          <div style="background: #f5f5f5; border-radius: 10px; padding: 15px;">
            <p id="uploadStatus" style="margin: 0 0 10px 0; font-weight: 600;"></p>
            <div style="background: #e0e0e0; border-radius: 10px; height: 8px; overflow: hidden;">
              <div id="uploadProgressBar" style="background: var(--primary-gradient); height: 100%; width: 0%; transition: width 0.3s;"></div>
            </div>
          </div>
        </div>

        <!-- Results -->
        <div id="uploadResults" style="display: none; margin: 20px 0;"></div>

        <!-- Buttons -->
        <div style="display: flex; gap: 10px; margin-top: 20px;">
          <button type="button" class="btn-primary" onclick="processBulkUpload()" style="flex: 1;">
            <i class="fas fa-upload"></i> Upload & Process
          </button>
          <button type="button" class="btn-secondary" onclick="closeBulkUploadModal()" style="flex: 1;">
            <i class="fas fa-times"></i> Cancel
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- Quick Edit Margin Modal -->
  <div id="marginModal" class="modal">
    <div class="modal-content" style="max-width: 400px;">
      <div class="modal-header">
        <h2><i class="fas fa-percentage"></i> Edit Margin</h2>
        <button class="modal-close" onclick="closeMarginModal()"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body">
        <form id="marginForm">
          <input type="hidden" id="marginItemId">
          
          <div class="form-group">
            <label>Item: <strong id="marginItemName"></strong></label>
          </div>

          <div class="form-group">
            <label><i class="fas fa-percentage"></i> New Margin (%)</label>
            <input type="number" id="marginValue" required min="0" max="100" step="0.1" placeholder="Enter new margin">
          </div>

          <button type="submit" class="btn-primary">
            <i class="fas fa-check"></i> Update Margin
          </button>
        </form>
      </div>
    </div>
  </div>

  <!-- Firebase SDK -->
  <script data-cfasync="false" src="/cdn-cgi/scripts/5c5dd728/cloudflare-static/email-decode.min.js"></script><script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-auth-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore-compat.js"></script>

  <script>
    // Firebase Configuration
    const firebaseConfig = {
      apiKey: "AIzaSyDbZVw5MVgrfFWAbTPByaUmKdbz0xPKofw",
      authDomain: "alcobina.firebaseapp.com",
      projectId: "alcobina",
      storageBucket: "alcobina.firebasestorage.app",
      messagingSenderId: "437821923842",
      appId: "1:437821923842:web:ea90ea7c256659ab3cfd1b",
      measurementId: "G-TCJLJRJ2B4"
    };

    // Initialize Firebase
    const app = firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();
    const db = firebase.firestore();

    // Configure Firestore settings BEFORE any operations (prevents warning)
    db.settings({
      cacheSizeBytes: firebase.firestore.CACHE_SIZE_UNLIMITED,
      ignoreUndefinedProperties: true
    });

    // Global State
    let currentUser = null;
    let currentBusiness = null;
    let currentBusinessName = null;
    let currentUserUID = null;
    let isMobile = window.innerWidth <= 768;
    let priceListData = [];
    let customersData = [];
    let inventoryData = [];
    let itemListData = [];

    // Check if user is logged in
    auth.onAuthStateChanged(async (user) => {
      if (user) {
        currentUser = user;
        currentUserUID = user.uid;
        console.log('✅ User signed in:', user.email, 'UID:', currentUserUID);
        
        // Load user's business data
        try {
          const userDoc = await db.collection('users').doc(user.uid).get();
          if (!userDoc.exists) {
            showError('User business data not found. Please contact support.');
            await auth.signOut();
            return;
          }
          
          const userData = userDoc.data();
          currentBusiness = userData.client_id || userData.business_id;
          currentBusinessName = userData.business_name || userData.company_name || 'Your Business';
          
          console.log('✅ Business loaded:', currentBusiness, currentBusinessName);
          
          document.getElementById('welcome-username').textContent = user.email;
          document.getElementById('business-name-display').textContent = currentBusinessName;
          document.getElementById('client-id-display').textContent = currentBusiness;
          document.getElementById('user-uid-display').textContent = currentUserUID;
          
          document.getElementById('loginPage').style.display = 'none';
          document.getElementById('appContainer').style.display = 'flex';
          
          // Load data
          await loadInventory();
          await loadItemList();
          await loadPriceList();
          await loadCustomers();
          
          // Note: syncPriceListFromInventory() only runs when user clicks "Sync Costs" button
          
        } catch (error) {
          console.error('❌ Error loading business data:', error);
          showError('Failed to load business data: ' + error.message);
          await auth.signOut();
        }
      } else {
        document.getElementById('loginPage').style.display = 'flex';
        document.getElementById('appContainer').style.display = 'none';
      }
    });

    // Login with better error handling
    document.getElementById('loginForm').addEventListener('submit', async (e) => {
      e.preventDefault();
      const email = document.getElementById('loginEmail').value.trim();
      const password = document.getElementById('loginPassword').value;
      const loginBtn = document.getElementById('loginBtn');
      
      // Disable button during login
      loginBtn.disabled = true;
      loginBtn.querySelector('span').textContent = 'Logging in...';
      
      try {
        await auth.signInWithEmailAndPassword(email, password);
      } catch (error) {
        console.error('Login error:', error);
        let errorMessage = 'Login failed. Please try again.';
        
        // Provide user-friendly error messages
        if (error.code === 'auth/user-not-found') {
          errorMessage = 'No account found with this email address.';
        } else if (error.code === 'auth/wrong-password') {
          errorMessage = 'Incorrect password. Please try again.';
        } else if (error.code === 'auth/invalid-email') {
          errorMessage = 'Invalid email address format.';
        } else if (error.code === 'auth/user-disabled') {
          errorMessage = 'This account has been disabled.';
        } else if (error.code === 'auth/too-many-requests') {
          errorMessage = 'Too many failed attempts. Please try again later.';
        } else if (error.code === 'auth/invalid-credential') {
          errorMessage = 'Invalid email or password. Please check your credentials.';
        } else {
          errorMessage = error.message;
        }
        
        showError(errorMessage);
        
        // Re-enable button
        loginBtn.disabled = false;
        loginBtn.querySelector('span').textContent = 'Login';
      }
    });

    function showError(message) {
      const errorDiv = document.getElementById('loginError');
      const errorText = document.getElementById('loginErrorText');
      errorText.textContent = message;
      errorDiv.classList.add('show');
      setTimeout(() => errorDiv.classList.remove('show'), 5000);
    }

    // Logout
    async function logout() {
      await auth.signOut();
      location.reload();
    }

    // Navigation
    function showWelcome() {
      hideAllSections();
      document.getElementById('welcome-section').style.display = 'flex';
      setActiveMenu(0);
    }

    function showInventory() {
      hideAllSections();
      document.getElementById('inventory-section').style.display = 'block';
      setActiveMenu(1);
    }

    function showPriceList() {
      hideAllSections();
      document.getElementById('price-list-section').style.display = 'block';
      setActiveMenu(3);
    }

    function showCustomers() {
      hideAllSections();
      document.getElementById('customers-section').style.display = 'block';
      setActiveMenu(5);
    }

    function showItemLookup() {
      hideAllSections();
      document.getElementById('item-lookup-section').style.display = 'block';
      setActiveMenu(6);
      loadItemLookup();
    }

    function showPOS() {
      hideAllSections();
      document.getElementById('pos-section').style.display = 'block';
      setActiveMenu(3);
      initializePOS();
    }

    function showComingSoon(feature, icon) {
      hideAllSections();
      document.getElementById('coming-soon-title').textContent = feature;
      document.getElementById('coming-soon-text').textContent = `${feature} is coming soon. Stay tuned!`;
      document.getElementById('coming-soon-icon').className = `fas fa-${icon}`;
      document.getElementById('coming-soon-section').style.display = 'block';
    }

    function hideAllSections() {
      document.getElementById('welcome-section').style.display = 'none';
      document.getElementById('inventory-section').style.display = 'none';
      document.getElementById('pos-section').style.display = 'none';
      document.getElementById('price-list-section').style.display = 'none';
      document.getElementById('customers-section').style.display = 'none';
      document.getElementById('item-lookup-section').style.display = 'none';
      document.getElementById('coming-soon-section').style.display = 'none';
    }

    function setActiveMenu(index) {
      const menuItems = document.querySelectorAll('.menu-item');
      menuItems.forEach((item, i) => {
        if (i === index) {
          item.classList.add('active');
        } else {
          item.classList.remove('active');
        }
      });
      if (isMobile) {
        document.getElementById('sidebar').classList.remove('show');
      }
    }

    function toggleSidebar() {
      document.getElementById('sidebar').classList.toggle('show');
    }

    // ==================== INVENTORY HISTORY ====================
    
    // Mode switching for inventory entry
    function setInventoryMode(mode) {
      document.getElementById('inventoryMode').value = mode;
      
      const btnNew = document.getElementById('btnNewItem');
      const btnExisting = document.getElementById('btnExistingItem');
      const searchSection = document.getElementById('existingItemSearch');
      const searchResults = document.getElementById('searchResults');
      
      if (mode === 'new') {
        btnNew.classList.add('active');
        btnExisting.classList.remove('active');
        searchSection.style.display = 'none';
        searchResults.style.display = 'none';
        
        // Enable all fields
        enableAllInventoryFields();
        
        // Clear form
        document.getElementById('inventoryForm').reset();
        document.getElementById('inventoryDocId').value = '';
        
        // Set current date
        const now = new Date();
        const localDateTime = new Date(now.getTime() - now.getTimezoneOffset() * 60000).toISOString().slice(0, 16);
        document.getElementById('inventoryPostingDate').value = localDateTime;
        
      } else {
        btnNew.classList.remove('active');
        btnExisting.classList.add('active');
        searchSection.style.display = 'block';
        
        // Clear form
        document.getElementById('inventoryForm').reset();
        document.getElementById('inventoryDocId').value = '';
        
        // Show all unique items immediately
        showAllUniqueItems();
      }
    }
    
    function enableAllInventoryFields() {
      const fields = [
        'inventoryItemNumber',
        'inventoryItemName',
        'inventoryBarcode',
        'inventoryDescription',
        'inventoryCategory',
        'inventoryUnitOfMeasure',
        'inventoryVendor'
      ];
      
      fields.forEach(fieldId => {
        const field = document.getElementById(fieldId);
        field.readOnly = false;
        field.disabled = false;
        field.classList.remove('readonly-field');
      });
    }
    
    function disableInventoryFields() {
      const fields = [
        'inventoryItemNumber',
        'inventoryItemName',
        'inventoryBarcode',
        'inventoryDescription',
        'inventoryCategory',
        'inventoryUnitOfMeasure',
        'inventoryVendor'
      ];
      
      fields.forEach(fieldId => {
        const field = document.getElementById(fieldId);
        field.readOnly = true;
        field.classList.add('readonly-field');
      });
    }
    
    function searchExistingInventory() {
      const searchTerm = document.getElementById('inventorySearchBox').value.toLowerCase().trim();
      const searchResults = document.getElementById('searchResults');
      
      console.log('🔍 Search term:', searchTerm);
      
      if (itemListData.length === 0) {
        searchResults.innerHTML = '<div style="padding: 12px; text-align: center; color: var(--text-gray);"><i class="fas fa-exclamation-triangle"></i><br>Item List not loaded yet. Please wait...</div>';
        searchResults.style.display = 'block';
        return;
      }
      
      // If search is empty, show all unique items
      if (searchTerm.length === 0) {
        showAllUniqueItems();
        return;
      }
      
      // If search term is less than 2 characters, still show all items
      if (searchTerm.length < 2) {
        showAllUniqueItems();
        return;
      }
      
      console.log('📊 itemListData length:', itemListData.length);
      console.log('📋 itemListData:', itemListData);
      
      
      // Filter from item_list (master item catalog)
      const filtered = itemListData.filter(item => {
        const matchName = item.item_name && item.item_name.toLowerCase().includes(searchTerm);
        const matchNumber = item.item_number && item.item_number.toLowerCase().includes(searchTerm);
        const matchDesc = item.description && item.description.toLowerCase().includes(searchTerm);
        const matchBarcode = (item.Barcode || item.barcode || '').toLowerCase().includes(searchTerm);
        return matchName || matchNumber || matchDesc || matchBarcode;
      });
      
      console.log('✅ Filtered results:', filtered.length, filtered);
      
      if (filtered.length === 0) {
        searchResults.innerHTML = '<div style="padding: 12px; text-align: center; color: var(--text-gray);">No items found matching "' + searchTerm + '"</div>';
        searchResults.style.display = 'block';
        return;
      }
      
      // Render search results from item_list with header
      let html = '<div style="padding: 8px; background: var(--primary-gradient); color: white; font-weight: 600; border-radius: var(--radius) var(--radius) 0 0;"><i class="fas fa-search"></i> Search Results (' + filtered.length + ')</div>';
      filtered.forEach(item => {
        html += `
          <div class="search-result-item" onclick='selectExistingItem(${JSON.stringify(item).replace(/'/g, "&apos;")})'>
            <strong>${item.item_name}</strong>
            <small>Item #: ${item.item_number} | Barcode: ${item.Barcode || item.barcode || 'N/A'} | Category: ${item.category || item.Category || 'N/A'} | Description: ${item.description || 'N/A'}</small>
          </div>
        `;
      });
      
      searchResults.innerHTML = html;
      searchResults.style.display = 'block';
    }
    function showAllUniqueItems() {
      const searchResults = document.getElementById('searchResults');
      
      console.log('📋 Showing all unique items from Item_list');
      
      if (itemListData.length === 0) {
        searchResults.innerHTML = '<div style="padding: 12px; text-align: center; color: var(--text-gray);"><i class="fas fa-exclamation-triangle"></i><br>Item List not loaded yet. Please wait...</div>';
        searchResults.style.display = 'block';
        return;
      }
      
      // Get unique items from itemListData (master Item_list)
      const uniqueItems = [];
      const seenItemNumbers = new Set();
      
      itemListData.forEach(item => {
        if (!seenItemNumbers.has(item.item_number)) {
          seenItemNumbers.add(item.item_number);
          uniqueItems.push(item);
        }
      });
      
      console.log('✅ Total unique items:', uniqueItems.length);
      
      if (uniqueItems.length === 0) {
        searchResults.innerHTML = '<div style="padding: 12px; text-align: center; color: var(--text-gray);">No items found in Item List</div>';
        searchResults.style.display = 'block';
        return;
      }
      
      // Render all unique items
      let html = '<div style="padding: 8px; background: var(--primary-gradient); color: white; font-weight: 600; border-radius: var(--radius) var(--radius) 0 0;"><i class="fas fa-list"></i> All Unique Items (' + uniqueItems.length + ')</div>';
      
      uniqueItems.forEach(item => {
        html += `
          <div class="search-result-item" onclick='selectExistingItem(${JSON.stringify(item).replace(/'/g, "&apos;")})'>
            <strong>${item.item_name}</strong>
            <small>Item #: ${item.item_number} | Barcode: ${item.Barcode || item.barcode || 'N/A'} | Category: ${item.category || item.Category || 'N/A'}</small>
          </div>
        `;
      });
      
      searchResults.innerHTML = html;
      searchResults.style.display = 'block';
    }
    
    function selectExistingItem(item) {
      // Hide search results
      document.getElementById('searchResults').style.display = 'none';
      document.getElementById('inventorySearchBox').value = item.item_name;
      
      // Fill form with item data from item_list
      document.getElementById('inventoryItemNumber').value = item.item_number;
      document.getElementById('inventoryItemName').value = item.item_name;
      
      // Map barcode from item_list (if exists) or leave empty
      document.getElementById('inventoryBarcode').value = item.Barcode || item.barcode || '';
      
      // Map description from item_list
      document.getElementById('inventoryDescription').value = item.description || item.Description || '';
      
      // Map category (handle both lowercase and uppercase)
      const category = item.category || item.Category || '';
      // Capitalize first letter to match dropdown options
      const categoryFormatted = category.charAt(0).toUpperCase() + category.slice(1).toLowerCase();
      document.getElementById('inventoryCategory').value = categoryFormatted;
      
      // Map unit_of_measure from item_list
      document.getElementById('inventoryUnitOfMeasure').value = item.unit_of_measure || '';
      
      // Map vendor (if exists in Item_list)
      document.getElementById('inventoryVendor').value = item.Vendor || item.vendor || '';
      
      // Make read-only fields uneditable
      disableInventoryFields();
      
      // Pre-fill unit cost from item_list (editable)
      document.getElementById('inventoryUnitCost').value = item.unit_cost || 0;
      
      // Clear quantity (user will enter current stock)
      document.getElementById('inventoryQuantity').value = '';
      
      // Set current date
      const now = new Date();
      const localDateTime = new Date(now.getTime() - now.getTimezoneOffset() * 60000).toISOString().slice(0, 16);
      document.getElementById('inventoryPostingDate').value = localDateTime;
      
      // Clear doc ID so it creates a new entry
      document.getElementById('inventoryDocId').value = '';
    }
    
    async function loadInventory() {
      if (!currentBusiness) {
        console.error('❌ No currentBusiness set');
        return;
      }

      console.log('🔍 Loading inventory for client_id:', currentBusiness);

      try {
        const snapshot = await db.collection('inventory_history')
          .where('client_id', '==', currentBusiness)
          .get();

        console.log('📊 Found', snapshot.size, 'inventory entries');

        inventoryData = [];
        snapshot.forEach(doc => {
          const data = doc.data();
          inventoryData.push({
            id: doc.id,
            ...data
          });
        });

        // Sort by posting_date descending (most recent first)
        inventoryData.sort((a, b) => {
          const dateA = a.posting_date ? a.posting_date.toDate() : new Date(0);
          const dateB = b.posting_date ? b.posting_date.toDate() : new Date(0);
          return dateB - dateA;
        });

        renderInventory(inventoryData);

      } catch (error) {
        console.error('❌ Error loading inventory:', error);
        document.getElementById('inventoryContainer').innerHTML = `
          <div class="empty-state">
            <i class="fas fa-exclamation-triangle"></i>
            <h3>Error Loading Inventory</h3>
            <p>Error: ${error.message}</p>
            <button class="btn-primary" onclick="loadInventory()"><i class="fas fa-sync"></i> Retry</button>
          </div>
        `;
      }
    }


    async function loadItemList() {
      if (!currentBusiness) {
        console.error('❌ No currentBusiness set');
        return;
      }

      console.log('🔍 Loading item_list for client_id:', currentBusiness);

      try {
        const snapshot = await db.collection('item_list')
          .where('client_id', '==', currentBusiness)
          .get();

        console.log('📊 Found', snapshot.size, 'items in item_list');

        itemListData = [];
        snapshot.forEach(doc => {
          const data = doc.data();
          itemListData.push({
            id: doc.id,
            ...data
          });
        });

        itemListData.sort((a, b) => {
          const nameA = (a.item_name || '').toLowerCase();
          const nameB = (b.item_name || '').toLowerCase();
          return nameA.localeCompare(nameB);
        });

        console.log('✅ item_list loaded:', itemListData.length, 'items');

      } catch (error) {
        console.error('❌ Error loading Item_list:', error);
      }
    }

    function renderInventory(data) {
      const container = document.getElementById('inventoryContainer');

      if (data.length === 0) {
        container.innerHTML = `
          <div class="empty-state">
            <i class="fas fa-boxes"></i>
            <h3>No Inventory Entries Found</h3>
            <p>Start by adding your first inventory entry</p>
            <button class="btn-primary" onclick="openAddInventoryModal()"><i class="fas fa-plus"></i> Add First Entry</button>
          </div>
        `;
        return;
      }

      let tableHTML = `
        <div class="data-table-container">
          <table class="data-table">
            <thead>
              <tr>
                <th>ITEM NUMBER</th>
                <th>ITEM NAME</th>
                <th>BARCODE</th>
                <th>CATEGORY</th>
                <th>QUANTITY</th>
                <th>UNIT COST</th>
                <th>UNIT</th>
                <th>VENDOR</th>
                <th>POSTING DATE</th>
                <th>ACTIONS</th>
              </tr>
            </thead>
            <tbody>
      `;

      data.forEach(item => {
        const postingDate = item.posting_date ? item.posting_date.toDate().toLocaleDateString() : 'N/A';
        const unitCost = parseFloat(item.unit_cost) || 0;
        
        tableHTML += `
          <tr>
            <td><span class="badge badge-primary">${item.item_number}</span></td>
            <td><strong>${item.item_name}</strong></td>
            <td>${item.Barcode || 'N/A'}</td>
            <td><span class="badge badge-info">${item.Category}</span></td>
            <td><span class="badge badge-success">${item.Quantity}</span></td>
            <td>$${unitCost.toFixed(2)}</td>
            <td>${item.unit_of_measure}</td>
            <td>${item.Vendor}</td>
            <td>${postingDate}</td>
            <td>
              <div class="table-actions">
                <button class="btn-edit-table" onclick='editInventory(${JSON.stringify(item).replace(/'/g, "&apos;")})'>
                  <i class="fas fa-edit"></i> Edit
                </button>
                <button class="btn-delete-table" onclick="deleteInventory('${item.id}', '${item.item_name}')">
                  <i class="fas fa-trash"></i>
                </button>
              </div>
            </td>
          </tr>
        `;
      });

      tableHTML += `
            </tbody>
          </table>
        </div>
      `;

      container.innerHTML = tableHTML;
    }

    function filterInventory() {
      const searchTerm = document.getElementById('inventorySearchInput').value.toLowerCase();
      
      const filtered = inventoryData.filter(item => 
        item.item_name.toLowerCase().includes(searchTerm) ||
        (item.item_number && item.item_number.toLowerCase().includes(searchTerm)) ||
        (item.Barcode && item.Barcode.toLowerCase().includes(searchTerm)) ||
        (item.Category && item.Category.toLowerCase().includes(searchTerm)) ||
        (item.Vendor && item.Vendor.toLowerCase().includes(searchTerm)) ||
        (item.Description && item.Description.toLowerCase().includes(searchTerm))
      );

      renderInventory(filtered);
    }

    function openAddInventoryModal() {
      document.getElementById('inventoryModalTitle').innerHTML = '<i class="fas fa-box"></i> Add Inventory Entry';
      document.getElementById('inventoryForm').reset();
      document.getElementById('inventoryDocId').value = '';
      
      // Show mode selection
      document.getElementById('inventoryModeSelection').style.display = 'block';
      
      // Reset to "New Item" mode by default
      setInventoryMode('new');
      
      document.getElementById('inventoryModal').classList.add('active');
    }

    function editInventory(item) {
      document.getElementById('inventoryModalTitle').innerHTML = '<i class="fas fa-edit"></i> Edit Inventory Entry';
      document.getElementById('inventoryDocId').value = item.id;
      
      // Hide mode selection when editing existing entry
      document.getElementById('inventoryModeSelection').style.display = 'none';
      document.getElementById('existingItemSearch').style.display = 'none';
      
      // Enable all fields for editing
      enableAllInventoryFields();
      
      document.getElementById('inventoryItemNumber').value = item.item_number;
      document.getElementById('inventoryItemName').value = item.item_name;
      document.getElementById('inventoryBarcode').value = item.Barcode || '';
      document.getElementById('inventoryDescription').value = item.Description || '';
      document.getElementById('inventoryCategory').value = item.Category || '';
      document.getElementById('inventoryQuantity').value = item.Quantity || 0;
      document.getElementById('inventoryUnitCost').value = item.unit_cost || 0;
      document.getElementById('inventoryUnitOfMeasure').value = item.unit_of_measure || '';
      document.getElementById('inventoryVendor').value = item.Vendor || '';
      
      // Convert Firebase timestamp to datetime-local format
      if (item.posting_date) {
        const date = item.posting_date.toDate();
        const localDateTime = new Date(date.getTime() - date.getTimezoneOffset() * 60000).toISOString().slice(0, 16);
        document.getElementById('inventoryPostingDate').value = localDateTime;
      }
      
      document.getElementById('inventoryModal').classList.add('active');
    }

    function closeInventoryModal() {
      document.getElementById('inventoryModal').classList.remove('active');
      document.getElementById('inventoryForm').reset();
    }

    document.getElementById('inventoryForm').addEventListener('submit', async (e) => {
      e.preventDefault();

      const docId = document.getElementById('inventoryDocId').value;
      const itemNumber = document.getElementById('inventoryItemNumber').value;
      const itemName = document.getElementById('inventoryItemName').value;
      const barcode = document.getElementById('inventoryBarcode').value;
      const description = document.getElementById('inventoryDescription').value;
      const category = document.getElementById('inventoryCategory').value;
      const quantity = parseInt(document.getElementById('inventoryQuantity').value);
      const unitCost = parseFloat(document.getElementById('inventoryUnitCost').value);
      const unitOfMeasure = document.getElementById('inventoryUnitOfMeasure').value;
      const vendor = document.getElementById('inventoryVendor').value;
      const postingDateStr = document.getElementById('inventoryPostingDate').value;
      
      // Convert datetime-local to Firebase Timestamp
      const postingDate = firebase.firestore.Timestamp.fromDate(new Date(postingDateStr));

      const inventoryData = {
        client_id: currentBusiness,
        item_number: itemNumber,
        item_name: itemName,
        Barcode: barcode,
        Description: description,
        Category: category,
        Quantity: quantity,
        unit_cost: unitCost,
        unit_of_measure: unitOfMeasure,
        Vendor: vendor,
        posting_date: postingDate
      };

      try {
        if (docId) {
          await db.collection('inventory_history').doc(docId).update(inventoryData);
          console.log('✅ Inventory entry updated:', docId);
        } else {
          await db.collection('inventory_history').add(inventoryData);
          console.log('✅ New inventory entry created');
        }

        closeInventoryModal();
        await loadInventory();
      } catch (error) {
        console.error('❌ Error saving inventory:', error);
        alert('Error: ' + error.message);
      }
    });

    async function deleteInventory(id, itemName) {
      if (confirm(`Delete inventory entry for "${itemName}"?`)) {
        try {
          await db.collection('inventory_history').doc(id).delete();
          console.log('✅ Inventory entry deleted:', id);
          await loadInventory();
        } catch (error) {
          console.error('❌ Error deleting inventory:', error);
          alert('Error: ' + error.message);
        }
      }
    }

    // ==================== CUSTOMERS ====================
    
    async function loadCustomers() {
      if (!currentBusiness) {
        console.error('❌ No currentBusiness set');
        return;
      }

      console.log('🔍 Loading customers for client_id:', currentBusiness);

      try {
        const snapshot = await db.collection('customers')
          .where('client_id', '==', currentBusiness)
          .get();

        console.log('📊 Found', snapshot.size, 'customer documents');

        customersData = [];
        snapshot.forEach(doc => {
          const data = doc.data();
          customersData.push({
            id: doc.id,
            customer_number: data.customer_number || doc.id,
            ...data
          });
        });

        customersData.sort((a, b) => {
          const nameA = (a.customer_name || '').toLowerCase();
          const nameB = (b.customer_name || '').toLowerCase();
          return nameA.localeCompare(nameB);
        });

        renderCustomers(customersData);

      } catch (error) {
        console.error('❌ Error loading customers:', error);
        document.getElementById('customersContainer').innerHTML = `
          <div class="empty-state">
            <i class="fas fa-exclamation-triangle"></i>
            <h3>Error Loading Customers</h3>
            <p>Error: ${error.message}</p>
            <button class="btn-primary" onclick="loadCustomers()"><i class="fas fa-sync"></i> Retry</button>
          </div>
        `;
      }
    }

    function renderCustomers(data) {
      const container = document.getElementById('customersContainer');

      if (data.length === 0) {
        container.innerHTML = `
          <div class="empty-state">
            <i class="fas fa-users"></i>
            <h3>No Customers Found</h3>
            <p>Start by adding your first customer</p>
            <button class="btn-primary" onclick="openAddCustomerModal()"><i class="fas fa-user-plus"></i> Add First Customer</button>
          </div>
        `;
        return;
      }

      let tableHTML = `
        <div class="data-table-container">
          <table class="data-table">
            <thead>
              <tr>
                <th>CUSTOMER NUMBER</th>
                <th>NAME</th>
                <th>TYPE</th>
                <th>EMAIL</th>
                <th>PHONE</th>
                <th>PARISH</th>
                <th>ADDRESS</th>
                <th>ACTIONS</th>
              </tr>
            </thead>
            <tbody>
      `;

      data.forEach(customer => {
        tableHTML += `
          <tr>
            <td><span class="badge badge-primary">${customer.customer_number || 'N/A'}</span></td>
            <td><strong>${customer.customer_name}</strong></td>
            <td>
              ${customer.customer_type ? `<span class="badge badge-secondary">${customer.customer_type}</span>` : '-'}
            </td>
            <td>
              ${customer.email ? `<a href="mailto:${customer.email}" style="color: #667eea;">${customer.email}</a>` : '-'}
            </td>
            <td>${customer.phone || '-'}</td>
            <td>${customer.parish || '-'}</td>
            <td>${customer.address || '-'}</td>
            <td>
              <div class="table-actions">
                <button class="btn-edit-table" onclick='editCustomer(${JSON.stringify(customer).replace(/'/g, "&apos;")})'>
                  <i class="fas fa-edit"></i> Edit
                </button>
                <button class="btn-delete-table" onclick="deleteCustomer('${customer.customer_number}', '${customer.customer_name}')">
                  <i class="fas fa-trash"></i>
                </button>
              </div>
            </td>
          </tr>
        `;
      });

      tableHTML += `
            </tbody>
          </table>
        </div>
      `;

      container.innerHTML = tableHTML;
    }

    function filterCustomers() {
      const searchTerm = document.getElementById('customerSearchInput').value.toLowerCase();
      
      const filtered = customersData.filter(customer => 
        customer.customer_name.toLowerCase().includes(searchTerm) ||
        (customer.customer_number && customer.customer_number.toLowerCase().includes(searchTerm)) ||
        (customer.phone && customer.phone.toLowerCase().includes(searchTerm)) ||
        (customer.email && customer.email.toLowerCase().includes(searchTerm)) ||
        (customer.customer_type && customer.customer_type.toLowerCase().includes(searchTerm)) ||
        (customer.parish && customer.parish.toLowerCase().includes(searchTerm))
      );

      renderCustomers(filtered);
    }

    async function openAddCustomerModal() {
      document.getElementById('customerModalTitle').innerHTML = '<i class="fas fa-user"></i> Add Customer';
      document.getElementById('customerForm').reset();
      document.getElementById('customerDocId').value = '';
      document.getElementById('customerNumber').value = '';
      document.getElementById('customerModal').classList.add('active');
    }

    function editCustomer(customer) {
      document.getElementById('customerModalTitle').innerHTML = '<i class="fas fa-edit"></i> Edit Customer';
      document.getElementById('customerDocId').value = customer.customer_number;
      document.getElementById('customerNumber').value = customer.customer_number;
      document.getElementById('customerName').value = customer.customer_name;
      document.getElementById('customerType').value = customer.customer_type || 'Retail';
      document.getElementById('customerPhone').value = customer.phone || '';
      document.getElementById('customerEmail').value = customer.email || '';
      document.getElementById('customerParish').value = customer.parish || '';
      document.getElementById('customerAddress').value = customer.address || '';
      document.getElementById('customerCreditLimit').value = customer.credit_limit || '';
      document.getElementById('customerNotes').value = customer.notes || '';
      document.getElementById('customerModal').classList.add('active');
    }

    function closeCustomerModal() {
      document.getElementById('customerModal').classList.remove('active');
      document.getElementById('customerForm').reset();
    }

    document.getElementById('customerForm').addEventListener('submit', async (e) => {
      e.preventDefault();

      const customerDocId = document.getElementById('customerDocId').value;
      const customerName = document.getElementById('customerName').value;
      const customerType = document.getElementById('customerType').value;
      const customerPhone = document.getElementById('customerPhone').value;
      const customerEmail = document.getElementById('customerEmail').value;
      const customerParish = document.getElementById('customerParish').value;
      const customerAddress = document.getElementById('customerAddress').value;
      const customerCreditLimit = parseFloat(document.getElementById('customerCreditLimit').value) || 0;
      const customerNotes = document.getElementById('customerNotes').value;

      try {
        if (customerDocId) {
          await db.collection('customers').doc(customerDocId).update({
            customer_name: customerName,
            customer_type: customerType,
            phone: customerPhone,
            email: customerEmail,
            parish: customerParish,
            address: customerAddress,
            credit_limit: customerCreditLimit,
            notes: customerNotes,
            updated_at: firebase.firestore.FieldValue.serverTimestamp()
          });
          console.log('✅ Customer updated:', customerDocId);
        } else {
          await db.runTransaction(async (transaction) => {
            const counterRef = db.collection('_metadata').doc(`${currentBusiness}_customer_counter`);
            const counterDoc = await transaction.get(counterRef);
            
            let nextNumber = 1;
            if (counterDoc.exists) {
              nextNumber = (counterDoc.data().current || 0) + 1;
            }

            const customerNumber = `CUST-${String(nextNumber).padStart(3, '0')}`;
            
            const existingCustomer = await transaction.get(db.collection('customers').doc(customerNumber));
            if (existingCustomer.exists) {
              throw new Error(`Customer number ${customerNumber} already exists!`);
            }

            transaction.set(db.collection('customers').doc(customerNumber), {
              client_id: currentBusiness,
              client_name: currentBusinessName,
              customer_number: customerNumber,
              customer_name: customerName,
              customer_type: customerType,
              phone: customerPhone,
              email: customerEmail,
              parish: customerParish,
              address: customerAddress,
              credit_limit: customerCreditLimit,
              notes: customerNotes,
              created_at: firebase.firestore.FieldValue.serverTimestamp(),
              updated_at: firebase.firestore.FieldValue.serverTimestamp()
            });

            transaction.set(counterRef, { current: nextNumber }, { merge: true });

            console.log('✅ New customer created with number:', customerNumber);
          });
        }

        closeCustomerModal();
        await loadCustomers();
      } catch (error) {
        console.error('❌ Error saving customer:', error);
        alert('Error: ' + error.message);
      }
    });

    async function deleteCustomer(customerNumber, customerName) {
      if (confirm(`Are you sure you want to delete customer "${customerName}"?`)) {
        try {
          await db.collection('customers').doc(customerNumber).delete();
          console.log('✅ Customer deleted:', customerNumber);
          await loadCustomers();
        } catch (error) {
          console.error('❌ Error deleting customer:', error);
          alert('Error deleting customer: ' + error.message);
        }
      }
    }

    // ==================== BULK UPLOAD ====================
    
    function showBulkUploadInstructions() {
      document.getElementById('bulkUploadModal').classList.add('active');
      // Reset form
      document.getElementById('bulkUploadFile').value = '';
      document.getElementById('uploadProgress').style.display = 'none';
      document.getElementById('uploadResults').style.display = 'none';
    }
    
    function closeBulkUploadModal() {
      document.getElementById('bulkUploadModal').classList.remove('active');
    }
    
    async function processBulkUpload() {
      const fileInput = document.getElementById('bulkUploadFile');
      const file = fileInput.files[0];
      
      if (!file) {
        alert('⚠️ Please select an Excel file first');
        return;
      }
      
      const fileName = file.name.toLowerCase();
      const validExtensions = ['.csv', '.xlsx', '.xls'];
      const isValidFile = validExtensions.some(ext => fileName.endsWith(ext));
      
      if (!isValidFile) {
        alert('⚠️ Please upload a CSV or Excel file (.csv, .xlsx, .xls)');
        return;
      }
      
      console.log('📁 Processing file:', file.name);
      
      // Show progress
      document.getElementById('uploadProgress').style.display = 'block';
      document.getElementById('uploadStatus').textContent = '📖 Reading file...';
      document.getElementById('uploadProgressBar').style.width = '20%';
      
      try {
        // Read Excel file using SheetJS (XLSX library)
        const data = await readExcelFile(file);
        
        console.log('📊 Parsed data:', data.length, 'rows');
        
        // Update progress
        document.getElementById('uploadStatus').textContent = '🔍 Validating data...';
        document.getElementById('uploadProgressBar').style.width = '40%';
        
        // Validate and process
        const results = await uploadCustomersToFirestore(data);
        
        // Show results
        displayUploadResults(results);
        
        // Reload customers
        await loadCustomers();
        
      } catch (error) {
        console.error('❌ Upload error:', error);
        alert('❌ Error: ' + error.message);
        document.getElementById('uploadProgress').style.display = 'none';
      }
    }
    
    async function readExcelFile(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        
        reader.onload = function(e) {
          try {
            const data = new Uint8Array(e.target.result);
            const workbook = XLSX.read(data, { type: 'array' });
            
            // Get first sheet
            const firstSheet = workbook.Sheets[workbook.SheetNames[0]];
            
            // Convert to JSON
            const jsonData = XLSX.utils.sheet_to_json(firstSheet);
            
            console.log('✅ File parsed:', jsonData.length, 'rows');
            resolve(jsonData);
          } catch (error) {
            reject(new Error('Failed to read file: ' + error.message));
          }
        };
        
        reader.onerror = function() {
          reject(new Error('Failed to load file'));
        };
        
        reader.readAsArrayBuffer(file);
      });
    }
    
    async function uploadCustomersToFirestore(data) {
      const results = {
        total: data.length,
        added: 0,
        skipped: 0,
        errors: 0,
        details: []
      };
      
      // Update progress
      document.getElementById('uploadStatus').textContent = '🔄 Processing customers...';
      document.getElementById('uploadProgressBar').style.width = '60%';
      
      // Get existing customers to check for duplicates
      const existingSnapshot = await db.collection('customers')
        .where('client_id', '==', currentBusiness)
        .get();
      
      const existingNames = new Set();
      existingSnapshot.forEach(doc => {
        const name = doc.data().customer_name;
        if (name) existingNames.add(name.toLowerCase().trim());
      });
      
      console.log('📋 Existing customers:', existingNames.size);
      
      // Get next customer number
      let customerCounter = existingSnapshot.size + 1;
      
      // Process each row
      for (let i = 0; i < data.length; i++) {
        const row = data[i];
        
        try {
          // Validate required field
          if (!row.customer_name || row.customer_name.trim() === '') {
            results.skipped++;
            results.details.push({
              row: i + 2,
              status: 'skipped',
              reason: 'Missing customer_name'
            });
            continue;
          }
          
          const customerName = row.customer_name.trim();
          
          // Check for duplicate
          if (existingNames.has(customerName.toLowerCase())) {
            results.skipped++;
            results.details.push({
              row: i + 2,
              name: customerName,
              status: 'skipped',
              reason: 'Duplicate name'
            });
            console.log('⏭️ Skipping duplicate:', customerName);
            continue;
          }
          
          // Generate customer number
          const customerNumber = `CUST-${String(customerCounter).padStart(3, '0')}`;
          
          // Create customer document
          const customerData = {
            customer_number: customerNumber,
            customer_name: customerName,
            customer_type: row.customer_type || 'Retail',
            phone: row.phone || '',
            email: row.email || '',
            parish: row.parish || '',
            address: row.address || '',
            credit_limit: parseFloat(row.credit_limit) || 0,
            notes: row.notes || '',
            client_id: currentBusiness,
            client_name: currentBusinessName || '',
            created_at: firebase.firestore.FieldValue.serverTimestamp(),
            updated_at: firebase.firestore.FieldValue.serverTimestamp()
          };
          
          // Add to Firestore
          await db.collection('customers').doc(customerNumber).set(customerData);
          
          // Track success
          existingNames.add(customerName.toLowerCase());
          customerCounter++;
          results.added++;
          results.details.push({
            row: i + 2,
            name: customerName,
            number: customerNumber,
            status: 'added'
          });
          
          console.log('✅ Added:', customerNumber, customerName);
          
          // Update progress
          const progress = 60 + (40 * (i + 1) / data.length);
          document.getElementById('uploadProgressBar').style.width = progress + '%';
          
        } catch (error) {
          results.errors++;
          results.details.push({
            row: i + 2,
            name: row.customer_name || 'Unknown',
            status: 'error',
            reason: error.message
          });
          console.error('❌ Error adding customer:', error);
        }
      }
      
      console.log('📊 Upload complete:', results);
      return results;
    }
    
    function displayUploadResults(results) {
      document.getElementById('uploadProgress').style.display = 'none';
      
      const resultsDiv = document.getElementById('uploadResults');
      resultsDiv.style.display = 'block';
      
      let html = '<div style="background: white; border-radius: 10px; padding: 20px; box-shadow: var(--shadow);">';
      
      // Summary
      html += '<h3 style="margin-top: 0; color: var(--primary-color);"><i class="fas fa-check-circle"></i> Upload Complete</h3>';
      html += '<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 15px; margin: 20px 0;">';
      
      html += `<div style="text-align: center; padding: 15px; background: #e8f5e9; border-radius: 8px;">
        <div style="font-size: 32px; font-weight: bold; color: #4caf50;">${results.added}</div>
        <div style="color: #666;">✅ Added</div>
      </div>`;
      
      html += `<div style="text-align: center; padding: 15px; background: #fff3e0; border-radius: 8px;">
        <div style="font-size: 32px; font-weight: bold; color: #ff9800;">${results.skipped}</div>
        <div style="color: #666;">⏭️ Skipped</div>
      </div>`;
      
      html += `<div style="text-align: center; padding: 15px; background: #ffebee; border-radius: 8px;">
        <div style="font-size: 32px; font-weight: bold; color: #f44336;">${results.errors}</div>
        <div style="color: #666;">❌ Errors</div>
      </div>`;
      
      html += '</div>';
      
      // Details
      if (results.details.length > 0) {
        html += '<details style="margin-top: 20px;"><summary style="cursor: pointer; font-weight: 600; padding: 10px; background: #f5f5f5; border-radius: 5px;">📋 View Details</summary>';
        html += '<div style="margin-top: 10px; max-height: 300px; overflow-y: auto;">';
        
        results.details.forEach(detail => {
          let icon = detail.status === 'added' ? '✅' : detail.status === 'skipped' ? '⏭️' : '❌';
          let color = detail.status === 'added' ? '#4caf50' : detail.status === 'skipped' ? '#ff9800' : '#f44336';
          
          html += `<div style="padding: 8px; margin: 5px 0; border-left: 3px solid ${color}; background: #f9f9f9;">
            ${icon} Row ${detail.row}: ${detail.name || 'Unknown'}
            ${detail.number ? ` → ${detail.number}` : ''}
            ${detail.reason ? ` (${detail.reason})` : ''}
          </div>`;
        });
        
        html += '</div></details>';
      }
      
      html += '</div>';
      
      resultsDiv.innerHTML = html;
    }
    
    // ==================== ITEM LOOKUP ====================
    
    async function loadItemLookup() {
      if (!currentBusiness) {
        console.error('❌ No currentBusiness set');
        return;
      }
      
      console.log('🔍 Loading item_list for lookup...');
      
      try {
        const snapshot = await db.collection('item_list')
          .where('client_id', '==', currentBusiness)
          .orderBy('item_name')
          .get();
        
        console.log('📦 Found', snapshot.size, 'items for lookup');
        
        const items = [];
        snapshot.forEach(doc => {
          items.push({ id: doc.id, ...doc.data() });
        });
        
        renderItemLookup(items);
      } catch (error) {
        console.error('❌ Error loading items:', error);
        document.getElementById('itemLookupContainer').innerHTML = `
          <div class="empty-state">
            <i class="fas fa-exclamation-triangle"></i>
            <p>Error loading items</p>
            <small>${error.message}</small>
          </div>
        `;
      }
    }
    
    function renderItemLookup(items) {
      const container = document.getElementById('itemLookupContainer');
      
      if (items.length === 0) {
        container.innerHTML = `
          <div class="empty-state">
            <i class="fas fa-search"></i>
            <p>No items found</p>
            <small>Add items to see them here</small>
          </div>
        `;
        return;
      }
      
      // Table layout like customers
      let html = `
        <div class="data-table">
          <table>
            <thead>
              <tr>
                <th>Item #</th>
                <th>Item Name</th>
                <th>Barcode</th>
                <th>Category</th>
                <th>Description</th>
                <th>Unit</th>
              </tr>
            </thead>
            <tbody>
      `;
      
      items.forEach(item => {
        const itemNumber = item.item_number || 'N/A';
        const itemName = item.item_name || 'Unknown';
        const barcode = item.Barcode || item.barcode || 'N/A';
        const category = item.category || 'N/A';
        const description = item.description || '-';
        const unit = item.unit_of_measure || 'N/A';
        
        html += `
          <tr>
            <td><strong>${itemNumber}</strong></td>
            <td>${itemName}</td>
            <td><code>${barcode}</code></td>
            <td><span class="badge">${category}</span></td>
            <td>${description}</td>
            <td>${unit}</td>
          </tr>
        `;
      });
      
      html += `
            </tbody>
          </table>
        </div>
      `;
      
      container.innerHTML = html;
    }
    
    function filterItemLookup() {
      const searchTerm = document.getElementById('itemLookupSearchInput').value.toLowerCase();
      
      const filtered = itemListData.filter(item => 
        (item.item_name && item.item_name.toLowerCase().includes(searchTerm)) ||
        (item.item_number && item.item_number.toLowerCase().includes(searchTerm)) ||
        (item.Barcode && item.Barcode.toLowerCase().includes(searchTerm)) ||
        (item.barcode && item.barcode.toLowerCase().includes(searchTerm)) ||
        (item.description && item.description.toLowerCase().includes(searchTerm)) ||
        (item.category && item.category.toLowerCase().includes(searchTerm))
      );
      
      renderItemLookup(filtered);
    }
    // ==================== POS SYSTEM ====================
    
    let posCart = [];
    let posCustomerData = {};
    let posItemsList = [];
    let currentTransactionId = null;
    
    async function initializePOS() {
      console.log('🛒 Initializing POS...');
      
      // Load customers
      await loadPOSCustomers();
      
      // Load items with prices
      await loadPOSItems();
      
      // Clear cart
      clearPOS();
    }
    
    async function loadPOSCustomers() {
      try {
        const snapshot = await db.collection('customers')
          .where('client_id', '==', currentBusiness)
          .orderBy('customer_name')
          .get();
        
        const select = document.getElementById('posCustomer');
        select.innerHTML = '<option value="">Select Customer...</option>';
        
        snapshot.forEach(doc => {
          const customer = doc.data();
          const option = document.createElement('option');
          option.value = customer.customer_number;
          option.textContent = `${customer.customer_name} (${customer.customer_number})`;
          option.dataset.customer = JSON.stringify(customer);
          select.appendChild(option);
        });
        
        console.log('✅ Loaded', snapshot.size, 'customers for POS');
      } catch (error) {
        console.error('❌ Error loading customers:', error);
      }
    }
    
    async function loadPOSItems() {
      try {
        // Load items from item_list
        const itemSnapshot = await db.collection('item_list')
          .where('client_id', '==', currentBusiness)
          .orderBy('item_name')
          .get();
        
        // Load prices from price_list
        const priceSnapshot = await db.collection('price_list')
          .where('client_id', '==', currentBusiness)
          .get();
        
        const priceMap = {};
        priceSnapshot.forEach(doc => {
          const price = doc.data();
          priceMap[price.item_number] = price;
        });
        
        // Load current stock from inventory_history
        const stockSnapshot = await db.collection('inventory_history')
          .where('client_id', '==', currentBusiness)
          .get();
        
        const stockMap = {};
        stockSnapshot.forEach(doc => {
          const inv = doc.data();
          if (!stockMap[inv.item_number]) {
            stockMap[inv.item_number] = 0;
          }
          stockMap[inv.item_number] += inv.Quantity || inv.quantity || 0;
        });
        
        posItemsList = [];
        const select = document.getElementById('posItemSelect');
        select.innerHTML = '<option value="">Select item...</option>';
        
        itemSnapshot.forEach(doc => {
          const item = doc.data();
          const priceData = priceMap[item.item_number] || {};
          const stock = stockMap[item.item_number] || 0;
          
          const itemData = {
            ...item,
            unit_cost: priceData.unit_cost || 0,
            margin: priceData.margin || 0,
            sell_price: priceData.unit_cost ? priceData.unit_cost * (1 + (priceData.margin || 0) / 100) : 0,
            stock: stock
          };
          
          posItemsList.push(itemData);
          
          const option = document.createElement('option');
          option.value = item.item_number;
          option.textContent = `${item.item_name} - $${itemData.sell_price.toFixed(2)} (Stock: ${stock})`;
          option.dataset.item = JSON.stringify(itemData);
          select.appendChild(option);
        });
        
        console.log('✅ Loaded', posItemsList.length, 'items for POS');
      } catch (error) {
        console.error('❌ Error loading items:', error);
      }
    }
    
    function handleCustomerChange() {
      const select = document.getElementById('posCustomer');
      const option = select.options[select.selectedIndex];
      
      if (!option || !option.dataset.customer) {
        document.getElementById('customerInfo').style.display = 'none';
        document.getElementById('posRepId').value = '1';
        posCustomerData = {};
        return;
      }
      
      posCustomerData = JSON.parse(option.dataset.customer);
      
      // Show customer info
      document.getElementById('customerEmail').textContent = posCustomerData.email || 'Not provided';
      document.getElementById('customerInfo').style.display = 'block';
      
      // Show credit limit for credit customers
      if (posCustomerData.customer_type !== 'Cash') {
        document.getElementById('creditLimitInfo').style.display = 'block';
        document.getElementById('customerCreditLimit').textContent = (posCustomerData.credit_limit || 0).toFixed(2);
      } else {
        document.getElementById('creditLimitInfo').style.display = 'none';
      }
      
      // Set rep ID
      document.getElementById('posRepId').value = posCustomerData.rep_id || 1;
      
      // Update transaction type default
      if (posCustomerData.customer_type === 'Cash') {
        document.getElementById('posTransactionType').value = 'Cash';
        handleTransactionTypeChange();
      }
      
      updateReceiptPreview();
    }
    
    function handleTransactionTypeChange() {
      const type = document.getElementById('posTransactionType').value;
      const termsSelect = document.getElementById('posPaymentTerms');
      
      if (type === 'Cash') {
        termsSelect.value = '0';
        termsSelect.disabled = true;
      } else {
        termsSelect.disabled = false;
        termsSelect.value = '14';
      }
      
      updateReceiptPreview();
    }
    
    function handleItemSelect() {
      const select = document.getElementById('posItemSelect');
      const option = select.options[select.selectedIndex];
      
      if (!option || !option.dataset.item) {
        document.getElementById('itemStock').style.display = 'none';
        return;
      }
      
      const item = JSON.parse(option.dataset.item);
      
      // Show stock
      document.getElementById('itemStockQty').textContent = item.stock;
      document.getElementById('itemStock').style.display = 'block';
    }
    
    function addItemToSale() {
      const select = document.getElementById('posItemSelect');
      const option = select.options[select.selectedIndex];
      
      if (!option || !option.dataset.item) {
        alert('⚠️ Please select an item');
        return;
      }
      
      const item = JSON.parse(option.dataset.item);
      const quantity = parseInt(document.getElementById('posQuantity').value) || 1;
      const discount = parseFloat(document.getElementById('posDiscount').value) || 0;
      
      // Validate quantity
      if (quantity <= 0) {
        alert('⚠️ Quantity must be greater than 0');
        return;
      }
      
      // Check stock
      if (quantity > item.stock) {
        alert(`⚠️ Insufficient stock! Only ${item.stock} available`);
        return;
      }
      
      // Calculate discounted price
      const sellPrice = item.sell_price;
      const discountedPrice = sellPrice * (1 - discount / 100);
      
      // Validate discount - cannot go below unit cost
      if (discountedPrice < item.unit_cost) {
        alert(`❌ Error: Discounted price ($${discountedPrice.toFixed(2)}) cannot be below unit cost ($${item.unit_cost.toFixed(2)})`);
        return;
      }
      
      // Add to cart
      const cartItem = {
        id: Date.now(),
        item_number: item.item_number,
        item_name: item.item_name,
        category: item.category,
        description: item.description,
        quantity: quantity,
        unit_cost: discountedPrice,
        original_price: sellPrice,
        discount: discount,
        subtotal: discountedPrice * quantity
      };
      
      posCart.push(cartItem);
      
      // Reset inputs
      document.getElementById('posItemSelect').value = '';
      document.getElementById('posQuantity').value = '1';
      document.getElementById('posDiscount').value = '0';
      document.getElementById('itemStock').style.display = 'none';
      
      renderCart();
      updateReceiptPreview();
      
      console.log('✅ Added to cart:', cartItem);
    }
    
    function renderCart() {
      const container = document.getElementById('posCartItems');
      
      if (posCart.length === 0) {
        container.innerHTML = `
          <div style="text-align: center; padding: 40px; color: #999;">
            <i class="fas fa-shopping-cart" style="font-size: 48px; margin-bottom: 10px;"></i>
            <p>No items added yet</p>
          </div>
        `;
        // Hide pre-sale actions when cart is empty
        document.getElementById('preSaleActions').style.display = 'none';
        return;
      }
      
      // Show pre-sale actions when cart has items
      document.getElementById('preSaleActions').style.display = 'flex';
      
      let html = '';
      
      posCart.forEach((item, index) => {
        const discountText = item.discount > 0 ? 
          `<span style="color: #f44336; font-size: 11px;">(${item.discount}% off)</span>` : '';
        
        html += `
          <div style="background: #f9f9f9; border-radius: 8px; padding: 12px; margin-bottom: 10px; border-left: 3px solid var(--primary-color);">
            <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 8px;">
              <div style="flex: 1;">
                <strong>${item.item_name}</strong> ${discountText}<br>
                <small style="color: #666;">${item.item_number} | ${item.category}</small>
              </div>
              <div style="text-align: right;">
                <strong style="font-size: 16px; color: var(--primary-color);">$${item.subtotal.toFixed(2)}</strong>
              </div>
            </div>
            <div style="display: flex; justify-content: space-between; align-items: center; font-size: 13px;">
              <span>${item.quantity} × $${item.unit_cost.toFixed(2)}</span>
              <div>
                <button onclick="editCartItem(${index})" style="background: #2196f3; color: white; border: none; padding: 4px 8px; border-radius: 4px; cursor: pointer; margin-right: 5px;">
                  <i class="fas fa-edit"></i>
                </button>
                <button onclick="voidCartItem(${index})" style="background: #f44336; color: white; border: none; padding: 4px 8px; border-radius: 4px; cursor: pointer;">
                  <i class="fas fa-trash"></i>
                </button>
              </div>
            </div>
          </div>
        `;
      });
      
      container.innerHTML = html;
    }
    
    function editCartItem(index) {
      const item = posCart[index];
      
      const newQty = prompt(`Edit quantity for ${item.item_name}:`, item.quantity);
      if (newQty === null) return;
      
      const quantity = parseInt(newQty);
      if (isNaN(quantity) || quantity <= 0) {
        alert('❌ Invalid quantity');
        return;
      }
      
      // Check stock
      const itemData = posItemsList.find(i => i.item_number === item.item_number);
      if (quantity > itemData.stock) {
        alert(`⚠️ Insufficient stock! Only ${itemData.stock} available`);
        return;
      }
      
      const newDiscount = prompt(`Edit discount % for ${item.item_name}:`, item.discount);
      if (newDiscount === null) return;
      
      const discount = parseFloat(newDiscount);
      if (isNaN(discount) || discount < 0 || discount > 100) {
        alert('❌ Invalid discount');
        return;
      }
      
      // Recalculate
      const discountedPrice = item.original_price * (1 - discount / 100);
      
      if (discountedPrice < itemData.unit_cost) {
        alert(`❌ Error: Discounted price ($${discountedPrice.toFixed(2)}) cannot be below unit cost ($${itemData.unit_cost.toFixed(2)})`);
        return;
      }
      
      posCart[index].quantity = quantity;
      posCart[index].discount = discount;
      posCart[index].unit_cost = discountedPrice;
      posCart[index].subtotal = discountedPrice * quantity;
      
      renderCart();
      updateReceiptPreview();
    }
    
    function voidCartItem(index) {
      if (confirm(`Remove ${posCart[index].item_name} from cart?`)) {
        posCart.splice(index, 1);
        renderCart();
        updateReceiptPreview();
      }
    }
    
    function voidAllItems() {
      if (posCart.length === 0) {
        alert('⚠️ Cart is already empty');
        return;
      }
      
      if (confirm('❌ Void all items in cart?')) {
        posCart = [];
        renderCart();
        updateReceiptPreview();
      }
    }
    
    function updateReceiptPreview() {
      const preview = document.getElementById('receiptPreview');
      
      if (posCart.length === 0 || !posCustomerData.customer_name) {
        preview.innerHTML = `
          <div style="text-align: center; color: #999; padding: 60px 20px;">
            <i class="fas fa-receipt" style="font-size: 48px; margin-bottom: 10px;"></i>
            <p>${!posCustomerData.customer_name ? 'Select customer and add items' : 'Add items to see receipt'}</p>
          </div>
        `;
        document.getElementById('receiptActions').style.display = 'none';
        return;
      }
      
      // Calculate totals
      const subtotal = posCart.reduce((sum, item) => sum + item.subtotal, 0);
      const totalDiscount = posCart.reduce((sum, item) => {
        const originalAmount = item.quantity * item.original_price;
        const discountedAmount = item.subtotal;
        return sum + (originalAmount - discountedAmount);
      }, 0);
      const gct = subtotal * 0.15; // 15% GCT
      const total = subtotal + gct;
      
      // Check credit limit
      const creditLimit = posCustomerData.credit_limit || 0;
      const transactionType = document.getElementById('posTransactionType').value;
      let creditWarning = '';
      
      if (transactionType === 'Credit' && total > creditLimit) {
        const overage = total - creditLimit;
        creditWarning = `
          <div style="background: #ffebee; border: 2px solid #f44336; border-radius: 5px; padding: 10px; margin: 10px 0; text-align: center;">
            <strong style="color: #f44336;">⚠️ CREDIT LIMIT EXCEEDED</strong><br>
            <span style="font-size: 13px;">Over by $${overage.toFixed(2)}</span><br>
            <small>Please adjust items or check outstanding bills</small>
          </div>
        `;
        
        document.getElementById('creditWarning').style.display = 'inline';
        document.getElementById('creditWarning').textContent = `⚠️ OVER LIMIT BY $${overage.toFixed(2)}`;
      } else {
        document.getElementById('creditWarning').style.display = 'none';
      }
      
      // Payment terms
      const paymentTerms = document.getElementById('posPaymentTerms').value;
      const dueDate = new Date();
      dueDate.setDate(dueDate.getDate() + parseInt(paymentTerms));
      
      let termsText = '';
      if (transactionType === 'Credit') {
        termsText = `
          <div style="text-align: center; margin: 10px 0; padding: 8px; background: #fff3e0; border-radius: 5px;">
            <strong>Payment Terms: ${paymentTerms} days</strong><br>
            <small>Due Date: ${dueDate.toLocaleDateString()}</small>
          </div>
        `;
      }
      
      // Build receipt
      let receipt = `
        <div style="border-bottom: 2px dashed #333; padding-bottom: 10px; margin-bottom: 10px;">
          <div style="text-align: center; font-weight: bold; font-size: 16px; margin-bottom: 5px;">
            ${currentBusinessName || 'ALCOBINA POS'}
          </div>
          <div style="text-align: center; font-size: 11px; color: #666;">
            ${new Date().toLocaleString()}
          </div>
        </div>
        
        <div style="margin-bottom: 10px; font-size: 12px;">
          <strong>Customer:</strong> ${posCustomerData.customer_name}<br>
          <strong>Customer #:</strong> ${posCustomerData.customer_number}<br>
          ${posCustomerData.email ? `<strong>Email:</strong> ${posCustomerData.email}<br>` : ''}
          <strong>Rep ID:</strong> ${document.getElementById('posRepId').value}<br>
          <strong>Type:</strong> ${transactionType}
        </div>
        
        ${termsText}
        ${creditWarning}
        
        <div style="border-bottom: 2px dashed #333; margin: 10px 0;"></div>
        
        <div style="margin-bottom: 10px;">
      `;
      
      // Items
      posCart.forEach(item => {
        const itemDiscountAmount = item.discount > 0 ? (item.quantity * item.original_price) - item.subtotal : 0;
        receipt += `
          <div style="margin-bottom: 8px;">
            <div style="font-weight: bold;">${item.item_name}</div>
            <div style="display: flex; justify-content: space-between; font-size: 11px;">
              <span>${item.quantity} × $${item.unit_cost.toFixed(2)}</span>
              <span>$${item.subtotal.toFixed(2)}</span>
            </div>
            ${item.discount > 0 ? `<div style="font-size: 10px; color: #f44336;">Discount: ${item.discount}% (-$${itemDiscountAmount.toFixed(2)})</div>` : ''}
          </div>
        `;
      });
      
      receipt += `
        </div>
        
        <div style="border-top: 2px dashed #333; padding-top: 10px; margin-top: 10px;">
          <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
            <span>Subtotal:</span>
            <span>$${subtotal.toFixed(2)}</span>
          </div>
          ${totalDiscount > 0 ? `
          <div style="display: flex; justify-content: space-between; margin-bottom: 5px; color: #f44336;">
            <span>Discount:</span>
            <span>-$${totalDiscount.toFixed(2)}</span>
          </div>
          ` : ''}
          <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
            <span>GCT (15%):</span>
            <span>$${gct.toFixed(2)}</span>
          </div>
          <div style="display: flex; justify-content: space-between; font-weight: bold; font-size: 16px; margin-top: 8px; padding-top: 8px; border-top: 2px solid #333;">
            <span>TOTAL:</span>
            <span>$${total.toFixed(2)}</span>
          </div>
        </div>
        
        <div style="text-align: center; margin-top: 15px; padding-top: 10px; border-top: 2px dashed #333; font-size: 11px; color: #666;">
          Thank you for your business!
        </div>
      `;
      
      preview.innerHTML = receipt;
      document.getElementById('receiptActions').style.display = 'none'; // Show after submit
    }
    
    function clearPOS() {
    function toggleSidebarCollapse() {
      const sidebar = document.getElementById('sidebar');
      sidebar.classList.toggle('collapsed');
      
      // Save state to localStorage
      const isCollapsed = sidebar.classList.contains('collapsed');
      localStorage.setItem('sidebarCollapsed', isCollapsed);
    }
    
    // Auto-collapse sidebar when menu item is clicked (on mobile/tablet)
    function handleMenuClick(callback) {
      // Execute the original function
      callback();
      
      // Auto-collapse on smaller screens
      if (window.innerWidth < 1024) {
        const sidebar = document.getElementById('sidebar');
        sidebar.classList.add('collapsed');
      }
    }
    
    // Restore sidebar state on page load
    window.addEventListener('DOMContentLoaded', () => {
      const savedState = localStorage.getItem('sidebarCollapsed');
      if (savedState === 'true') {
        document.getElementById('sidebar').classList.add('collapsed');
      }
    });
    // Pre-sale actions: Quote, PDF, Email, Print
    function showPreSaleActions() {
      if (!posCustomerData.customer_number) {
        alert('⚠️ Please select a customer');
        return;
      }
      
      if (posCart.length === 0) {
        alert('⚠️ Please add items to cart');
        return;
      }
      
      const actions = `
        Choose an action:
        
        1. Send Quote (Email - not a receipt, prices subject to change)
        2. Complete Sale & Generate Receipt
      `;
      
      // Show action buttons
      document.getElementById('preSaleActions').style.display = 'flex';
    }
    
    async function sendQuote() {
      if (!posCustomerData.email) {
        alert('⚠️ Customer email not available');
        return;
      }
      
      const subtotal = posCart.reduce((sum, item) => sum + item.subtotal, 0);
      const gct = subtotal * 0.15;
      const total = subtotal + gct;
      
      const quoteHTML = generateQuoteHTML(subtotal, gct, total);
      
      // In production, this would send via email service
      const mailto = `mailto:${posCustomerData.email}?subject=Quote from ${currentBusinessName || 'ALCOBINA'}&body=Please find your quote attached.`;
      
      // For now, show quote in new window
      const quoteWindow = window.open('', '_blank');
      quoteWindow.document.write(quoteHTML);
      quoteWindow.document.close();
      
      alert(`✅ Quote generated!\n\nOpening quote window...\nCustomer: ${posCustomerData.customer_name}\nEmail: ${posCustomerData.email}`);
    }
    
    function generateQuoteHTML(subtotal, gct, total) {
      const today = new Date().toLocaleDateString();
      
      let itemsHTML = '';
      posCart.forEach(item => {
        const discountAmount = item.discount || 0;
        itemsHTML += `
          <tr>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">${item.item_name}</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd; text-align: center;">${item.quantity}</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd; text-align: right;">$${item.unit_cost.toFixed(2)}</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd; text-align: right;">$${discountAmount.toFixed(2)}</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd; text-align: right;">$${item.subtotal.toFixed(2)}</td>
          </tr>
        `;
      });
      
      return `
        <!DOCTYPE html>
        <html>
        <head>
          <title>QUOTATION</title>
          <style>
            body { font-family: Arial, sans-serif; max-width: 800px; margin: 40px auto; padding: 20px; }
            .watermark { 
              position: fixed;
              top: 50%;
              left: 50%;
              transform: translate(-50%, -50%) rotate(-45deg);
              font-size: 120px;
              font-weight: bold;
              color: rgba(255, 0, 0, 0.1);
              z-index: -1;
              pointer-events: none;
            }
            .header { text-align: center; margin-bottom: 30px; border-bottom: 3px solid #333; padding-bottom: 20px; }
            .disclaimer { 
              background: #fff3cd; 
              border: 2px solid #ffc107; 
              padding: 15px; 
              margin: 20px 0; 
              border-radius: 5px;
              font-weight: bold;
              color: #856404;
            }
            table { width: 100%; border-collapse: collapse; margin: 20px 0; }
            th { background: #333; color: white; padding: 10px; text-align: left; }
            .totals { text-align: right; margin-top: 20px; font-size: 16px; }
            .totals div { margin: 5px 0; }
          </style>
        </head>
        <body>
          <div class="watermark">QUOTATION</div>
          
          <div class="header">
            <h1>QUOTATION</h1>
            <h2>${currentBusinessName || 'ALCOBINA'}</h2>
            <p>Date: ${today}</p>
          </div>
          
          <div class="disclaimer">
            ⚠️ THIS IS NOT A CASH RECEIPT
            <br>
            PRICES ARE SUBJECT TO CHANGE WITHOUT NOTICE
          </div>
          
          <div style="margin: 20px 0;">
            <strong>Customer:</strong> ${posCustomerData.customer_name}<br>
            <strong>Customer #:</strong> ${posCustomerData.customer_number}<br>
            <strong>Email:</strong> ${posCustomerData.email || 'N/A'}
          </div>
          
          <table>
            <thead>
              <tr>
                <th>Item</th>
                <th style="text-align: center;">Qty</th>
                <th style="text-align: right;">Unit Price</th>
                <th style="text-align: right;">Discount</th>
                <th style="text-align: right;">Subtotal</th>
              </tr>
            </thead>
            <tbody>
              ${itemsHTML}
            </tbody>
          </table>
          
          <div class="totals">
            <div><strong>Subtotal:</strong> $${subtotal.toFixed(2)}</div>
            <div><strong>GCT (15%):</strong> $${gct.toFixed(2)}</div>
            <div style="font-size: 20px; margin-top: 10px; padding-top: 10px; border-top: 2px solid #333;">
              <strong>TOTAL:</strong> $${total.toFixed(2)}
            </div>
          </div>
          
          <div style="margin-top: 40px; text-align: center; color: #666;">
            <p>Thank you for your interest!</p>
            <p style="font-size: 12px;">This is a quotation only. Final invoice will be issued upon purchase.</p>
          </div>
        </body>
        </html>
      `;
    }
    
    function generateReceiptHTML(isCopy = false) {
      const subtotal = posCart.reduce((sum, item) => sum + item.subtotal, 0);
      const gct = subtotal * 0.15;
      const total = subtotal + gct;
      const today = new Date().toLocaleDateString();
      const transactionType = document.getElementById('posTransactionType').value;
      const paymentTerms = parseInt(document.getElementById('posPaymentTerms').value);
      
      let dueDate = '';
      if (transactionType === 'Credit' && paymentTerms > 0) {
        const due = new Date();
        due.setDate(due.getDate() + paymentTerms);
        dueDate = due.toLocaleDateString();
      }
      
      let itemsHTML = '';
      posCart.forEach(item => {
        const discountAmount = item.discount || 0;
        itemsHTML += `
          <tr>
            <td style="padding: 8px; border-bottom: 1px solid #ddd;">${item.item_name}</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd; text-align: center;">${item.quantity}</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd; text-align: right;">$${item.unit_cost.toFixed(2)}</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd; text-align: right;">$${discountAmount.toFixed(2)}</td>
            <td style="padding: 8px; border-bottom: 1px solid #ddd; text-align: right;">$${item.subtotal.toFixed(2)}</td>
          </tr>
        `;
      });
      
      const copyWatermark = isCopy ? '<div class="watermark">COPY</div>' : '';
      
      return `
        <!DOCTYPE html>
        <html>
        <head>
          <title>Receipt - ${currentTransactionId}</title>
          <style>
            body { font-family: Arial, sans-serif; max-width: 800px; margin: 40px auto; padding: 20px; }
            .watermark { 
              position: fixed;
              top: 50%;
              left: 50%;
              transform: translate(-50%, -50%) rotate(-45deg);
              font-size: 150px;
              font-weight: bold;
              color: rgba(0, 0, 255, 0.1);
              z-index: -1;
              pointer-events: none;
              letter-spacing: 20px;
            }
            .header { text-align: center; margin-bottom: 30px; border-bottom: 3px solid #333; padding-bottom: 20px; }
            table { width: 100%; border-collapse: collapse; margin: 20px 0; }
            th { background: #333; color: white; padding: 10px; text-align: left; }
            .totals { text-align: right; margin-top: 20px; font-size: 16px; }
            .totals div { margin: 5px 0; }
            @media print {
              button { display: none; }
            }
          </style>
        </head>
        <body>
          ${copyWatermark}
          
          <div class="header">
            <h1>RECEIPT</h1>
            <h2>${currentBusinessName || 'ALCOBINA'}</h2>
            <p>Date: ${today}</p>
            <p><strong>Transaction ID: ${currentTransactionId}</strong></p>
          </div>
          
          <div style="margin: 20px 0;">
            <strong>Customer:</strong> ${posCustomerData.customer_name}<br>
            <strong>Customer #:</strong> ${posCustomerData.customer_number}<br>
            <strong>Type:</strong> ${transactionType}<br>
            ${dueDate ? `<strong>Due Date:</strong> ${dueDate}<br>` : ''}
            <strong>Rep ID:</strong> ${document.getElementById('posRepId').value}
          </div>
          
          <table>
            <thead>
              <tr>
                <th>Item</th>
                <th style="text-align: center;">Qty</th>
                <th style="text-align: right;">Unit Price</th>
                <th style="text-align: right;">Discount</th>
                <th style="text-align: right;">Subtotal</th>
              </tr>
            </thead>
            <tbody>
              ${itemsHTML}
            </tbody>
          </table>
          
          <div class="totals">
            <div><strong>Subtotal:</strong> $${subtotal.toFixed(2)}</div>
            <div><strong>GCT (15%):</strong> $${gct.toFixed(2)}</div>
            <div style="font-size: 20px; margin-top: 10px; padding-top: 10px; border-top: 2px solid #333;">
              <strong>TOTAL:</strong> $${total.toFixed(2)}
            </div>
          </div>
          
          <div style="margin-top: 40px; text-align: center; color: #666;">
            <p>Thank you for your business!</p>
            <p style="font-size: 12px;">Powered by ALCOBINA</p>
          </div>
          
          <div style="margin-top: 20px; text-align: center;">
            <button onclick="window.print()" style="padding: 10px 20px; font-size: 16px; cursor: pointer;">
              🖨️ Print Receipt
            </button>
          </div>
        </body>
        </html>
      `;
    }
    
    function generatePDFReceipt() {
      const receiptWindow = window.open('', '_blank');
      receiptWindow.document.write(generateReceiptHTML(true)); // true = show COPY watermark
      receiptWindow.document.close();
    }
    
    function emailReceiptCopy() {
      if (!posCustomerData.email) {
        alert('⚠️ Customer email not available');
        return;
      }
      
      // In production, this would send via email service
      const receiptWindow = window.open('', '_blank');
      receiptWindow.document.write(generateReceiptHTML(true)); // true = show COPY watermark
      receiptWindow.document.close();
      
      alert(`✅ Receipt (COPY) opened for email!\n\nCustomer: ${posCustomerData.customer_name}\nEmail: ${posCustomerData.email}\n\nNote: Email integration requires server-side setup.`);
    }
    
    function printReceipt() {
      const receiptWindow = window.open('', '_blank');
      receiptWindow.document.write(generateReceiptHTML(false)); // false = no watermark for first print
      receiptWindow.document.close();
      receiptWindow.onload = function() {
        receiptWindow.print();
      };
    }
      posCart = [];
      posCustomerData = {};
      currentTransactionId = null;
      
      document.getElementById('posCustomer').value = '';
      document.getElementById('posRepId').value = '1';
      document.getElementById('posTransactionType').value = 'Cash';
      document.getElementById('posPaymentTerms').value = '0';
      document.getElementById('posPaymentTerms').disabled = true;
      document.getElementById('posItemSelect').value = '';
      document.getElementById('posQuantity').value = '1';
      document.getElementById('posDiscount').value = '0';
      document.getElementById('customerInfo').style.display = 'none';
      document.getElementById('itemStock').style.display = 'none';
      
      renderCart();
      updateReceiptPreview();
      
      console.log('🔄 POS cleared');
    }

    
    async function submitSale() {
      // Validate
      if (!posCustomerData.customer_number) {
        alert('⚠️ Please select a customer');
        return;
      }
      
      if (posCart.length === 0) {
        alert('⚠️ Please add items to cart');
        return;
      }
      
      const transactionType = document.getElementById('posTransactionType').value;
      const subtotal = posCart.reduce((sum, item) => sum + item.subtotal, 0);
      const gct = subtotal * 0.15;
      const total = subtotal + gct;
      
      // Check credit limit
      if (transactionType === 'Credit') {
        const creditLimit = posCustomerData.credit_limit || 0;
        if (total > creditLimit) {
          const proceed = confirm(
            `⚠️ WARNING: Total ($${total.toFixed(2)}) exceeds credit limit ($${creditLimit.toFixed(2)}).\n\n` +
            `Consider adjusting items to stay under limit.\n\n` +
            `Do you want to proceed anyway?`
          );
          if (!proceed) return;
        }
      }
      
      try {
        console.log('💾 Submitting sale...');
        
        // Generate transaction ID
        const txnSnapshot = await db.collection('pos_transactions')
          .where('client_id', '==', currentBusiness)
          .orderBy('created_date', 'desc')
          .limit(1)
          .get();
        
        let txnCounter = 1;
        if (!txnSnapshot.empty) {
          const lastTxn = txnSnapshot.docs[0].data();
          if (lastTxn.transaction_id) {
            const match = lastTxn.transaction_id.match(/INV-(\d+)/);
            if (match) {
              txnCounter = parseInt(match[1]) + 1;
            }
          }
        }
        
        currentTransactionId = `INV-${String(txnCounter).padStart(4, '0')}`;
        
        // Save each line item as a transaction
        const batch = db.batch();
        const paymentTerms = parseInt(document.getElementById('posPaymentTerms').value);
        
        for (const item of posCart) {
          const txnData = {
            transaction_id: currentTransactionId,
            transaction_type: transactionType,
            transaction_action: 'Sale',
            customer_number: posCustomerData.customer_number,
            customer_name: posCustomerData.customer_name,
            rep_id: parseInt(document.getElementById('posRepId').value),
            item_number: item.item_number,
            item_name: item.item_name,
            category: item.category,
            description: item.description,
            quantity: item.quantity,
            unit_cost: item.unit_cost,
            discount: item.discount,
            subtotal: item.subtotal,
            gct: 15,
            total: item.subtotal * 1.15,
            payment_term: paymentTerms,
            account_type: transactionType.toLowerCase(),
            client_id: currentBusiness,
            client_name: currentBusinessName || '',
            created_date: firebase.firestore.FieldValue.serverTimestamp()
          };
          
          const docRef = db.collection('pos_transactions').doc();
          batch.set(docRef, txnData);
        }
        
        await batch.commit();
        
        // ✅ DEDUCT FROM CREDIT LIMIT if Credit transaction
        if (transactionType === 'Credit') {
          const customerRef = db.collection('customers')
            .where('client_id', '==', currentBusiness)
            .where('customer_number', '==', posCustomerData.customer_number);
          
          const customerSnapshot = await customerRef.get();
          if (!customerSnapshot.empty) {
            const customerDoc = customerSnapshot.docs[0];
            const currentCreditLimit = customerDoc.data().credit_limit || 0;
            const newCreditLimit = currentCreditLimit - total;
            
            await customerDoc.ref.update({
              credit_limit: newCreditLimit,
              updated_at: firebase.firestore.FieldValue.serverTimestamp()
            });
            
            console.log(`✅ Credit limit updated: ${currentCreditLimit} → ${newCreditLimit}`);
          }
        }
        
        console.log('✅ Sale submitted:', currentTransactionId);
        
        alert(`✅ Sale Complete!\n\nTransaction ID: ${currentTransactionId}\nTotal: $${total.toFixed(2)}`);
        
        // Auto-clear and reset for new sale
        clearPOS();
        
      } catch (error) {
        console.error('❌ Error submitting sale:', error);
        alert('❌ Error: ' + error.message);
      }
    }
    
    function emailReceipt() {
      if (!currentTransactionId) {
        alert('⚠️ Please complete a sale first');
        return;
      }
      
      if (!posCustomerData.email) {
        alert('⚠️ Customer email not available');
        return;
      }
      
      alert(`📧 Email functionality coming soon!\n\nWould send receipt for ${currentTransactionId} to:\n${posCustomerData.email}`);
    }
    
    function downloadReceiptPDF() {
      if (!currentTransactionId) {
        alert('⚠️ Please complete a sale first');
        return;
      }
      
      alert(`📄 PDF download coming soon!\n\nTransaction: ${currentTransactionId}`);
    }
    
    // Search Transactions
    function openSearchTransactions() {
      document.getElementById('searchTransactionsModal').classList.add('active');
      loadAllTransactions();
    }
    
    function closeSearchTransactions() {
      document.getElementById('searchTransactionsModal').classList.remove('active');
    }
    
    async function loadAllTransactions() {
      try {
        console.log('🔍 Loading transactions...');
        
        const snapshot = await db.collection('pos_transactions')
          .where('client_id', '==', currentBusiness)
          .orderBy('created_date', 'desc')
          .limit(100)
          .get();
        
        const transactions = [];
        snapshot.forEach(doc => {
          transactions.push({ id: doc.id, ...doc.data() });
        });
        
        // Group by transaction_id
        const grouped = {};
        transactions.forEach(txn => {
          if (!grouped[txn.transaction_id]) {
            grouped[txn.transaction_id] = [];
          }
          grouped[txn.transaction_id].push(txn);
        });
        
        renderTransactionResults(grouped);
        
      } catch (error) {
        console.error('❌ Error loading transactions:', error);
        document.getElementById('transactionResults').innerHTML = `
          <div style="text-align: center; padding: 40px; color: #f44336;">
            <i class="fas fa-exclamation-triangle" style="font-size: 48px; margin-bottom: 10px;"></i>
            <p>Error loading transactions</p>
            <small>${error.message}</small>
          </div>
        `;
      }
    }
    
    function renderTransactionResults(grouped) {
      const container = document.getElementById('transactionResults');
      
      if (Object.keys(grouped).length === 0) {
        container.innerHTML = `
          <div style="text-align: center; padding: 40px; color: #999;">
            <i class="fas fa-receipt" style="font-size: 48px; margin-bottom: 10px;"></i>
            <p>No transactions found</p>
          </div>
        `;
        return;
      }
      
      let html = '';
      
      Object.keys(grouped).forEach(txnId => {
        const items = grouped[txnId];
        const first = items[0];
        const total = items.reduce((sum, item) => sum + item.total, 0);
        const isVoided = first.transaction_action === 'Void';
        const isRefund = first.transaction_action === 'Refund';
        
        const statusBadge = isVoided ? 
          '<span style="background: #f44336; color: white; padding: 2px 8px; border-radius: 4px; font-size: 11px;">VOID</span>' :
          isRefund ?
          '<span style="background: #ff9800; color: white; padding: 2px 8px; border-radius: 4px; font-size: 11px;">REFUND</span>' :
          '<span style="background: #4caf50; color: white; padding: 2px 8px; border-radius: 4px; font-size: 11px;">SALE</span>';
        
        html += `
          <div style="background: white; border-radius: 8px; padding: 15px; margin-bottom: 15px; box-shadow: var(--shadow); border-left: 4px solid ${isVoided || isRefund ? '#f44336' : '#4caf50'};">
            <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 10px;">
              <div>
                <strong style="font-size: 16px;">${txnId}</strong> ${statusBadge}<br>
                <small style="color: #666;">
                  ${first.customer_name} (${first.customer_number}) | 
                  ${first.created_date ? new Date(first.created_date.toDate()).toLocaleString() : 'N/A'}
                </small>
              </div>
              <div style="text-align: right;">
                <strong style="font-size: 18px; color: ${isVoided || isRefund ? '#f44336' : '#4caf50'};">
                  ${isRefund ? '-' : ''}$${Math.abs(total).toFixed(2)}
                </strong><br>
                <small style="color: #666;">${first.transaction_type}</small>
              </div>
            </div>
            
            <details>
              <summary style="cursor: pointer; color: var(--primary-color); font-size: 13px;">
                <i class="fas fa-list"></i> ${items.length} item(s) - View Details
              </summary>
              <div style="margin-top: 10px; padding-top: 10px; border-top: 1px solid #eee;">
                ${items.map(item => `
                  <div style="padding: 5px 0; font-size: 13px;">
                    ${item.item_name} - ${item.quantity} × $${item.unit_cost.toFixed(2)} = $${item.subtotal.toFixed(2)}
                    ${item.discount > 0 ? `<span style="color: #f44336;">(${item.discount}% off)</span>` : ''}
                  </div>
                `).join('')}
              </div>
            </details>
            
            ${!isVoided && !isRefund ? `
              <div style="margin-top: 15px; padding-top: 15px; border-top: 1px solid #eee; display: flex; gap: 10px;">
                <button onclick="voidTransaction('${txnId}')" style="flex: 1; background: #f44336; color: white; border: none; padding: 8px; border-radius: 5px; cursor: pointer;">
                  <i class="fas fa-ban"></i> Void
                </button>
                <button onclick="refundTransaction('${txnId}')" style="flex: 1; background: #ff9800; color: white; border: none; padding: 8px; border-radius: 5px; cursor: pointer;">
                  <i class="fas fa-undo"></i> Refund
                </button>
                <button onclick="viewReceiptPDF('${txnId}')" style="flex: 1; background: #2196f3; color: white; border: none; padding: 8px; border-radius: 5px; cursor: pointer;">
                  <i class="fas fa-file-pdf"></i> PDF
                </button>
              </div>
            ` : ''}
          </div>
        `;
      });
      
      container.innerHTML = html;
    }
    
    function filterTransactions() {
      // Simple filter for now
      const searchTerm = document.getElementById('transactionSearchInput').value.toLowerCase();
      // In production, you'd filter the loaded transactions
      console.log('Filtering by:', searchTerm);
    }
    
    async function voidTransaction(txnId) {
      if (!confirm(`❌ Void transaction ${txnId}?\n\nThis will mark all items as voided.`)) {
        return;
      }
      
      try {
        console.log('🔄 Voiding transaction:', txnId);
        
        const snapshot = await db.collection('pos_transactions')
          .where('transaction_id', '==', txnId)
          .where('client_id', '==', currentBusiness)
          .get();
        
        const batch = db.batch();
        snapshot.forEach(doc => {
          batch.update(doc.ref, {
            transaction_action: 'Void',
            voided_date: firebase.firestore.FieldValue.serverTimestamp()
          });
        });
        
        await batch.commit();
        
        alert(`✅ Transaction ${txnId} voided`);
        loadAllTransactions();
        
      } catch (error) {
        console.error('❌ Error voiding transaction:', error);
        alert('❌ Error: ' + error.message);
      }
    }
    
    async function refundTransaction(txnId) {
      if (!confirm(`💰 Process refund for ${txnId}?\n\nThis will create a negative transaction.`)) {
        return;
      }
      
      try {
        console.log('💰 Processing refund:', txnId);
        
        // Get original transaction
        const snapshot = await db.collection('pos_transactions')
          .where('transaction_id', '==', txnId)
          .where('client_id', '==', currentBusiness)
          .get();
        
        if (snapshot.empty) {
          alert('❌ Transaction not found');
          return;
        }
        
        // Generate refund transaction ID
        const refundTxnId = `REF-${txnId}`;
        
        // Create negative transactions
        const batch = db.batch();
        
        snapshot.forEach(doc => {
          const original = doc.data();
          
          const refundData = {
            ...original,
            transaction_id: refundTxnId,
            transaction_action: 'Refund',
            quantity: -Math.abs(original.quantity),
            subtotal: -Math.abs(original.subtotal),
            total: -Math.abs(original.total),
            original_transaction_id: txnId,
            refund_date: firebase.firestore.FieldValue.serverTimestamp(),
            created_date: firebase.firestore.FieldValue.serverTimestamp()
          };
          
          const refundRef = db.collection('pos_transactions').doc();
          batch.set(refundRef, refundData);
        });
        
        await batch.commit();
        
        alert(`✅ Refund processed!\n\nRefund ID: ${refundTxnId}`);
        loadAllTransactions();
        
      } catch (error) {
        console.error('❌ Error processing refund:', error);
        alert('❌ Error: ' + error.message);
      }
    }
    
    function viewReceiptPDF(txnId) {
      alert(`📄 PDF for ${txnId} coming soon!`);
    }


    // ==================== PRICE LIST ====================
    
    async function loadPriceList() {
      if (!currentBusiness) {
        console.error('❌ No currentBusiness set');
        return;
      }

      console.log('🔍 Loading price_list for client_id:', currentBusiness);

      try {
        const snapshot = await db.collection('price_list')
          .where('client_id', '==', currentBusiness)
          .get();

        console.log('📊 Found', snapshot.size, 'price_list items');

        priceListData = [];
        snapshot.forEach(doc => {
          const data = doc.data();
          priceListData.push({
            id: doc.id,
            ...data
          });
        });

        priceListData.sort((a, b) => {
          const nameA = (a.item_name || '').toLowerCase();
          const nameB = (b.item_name || '').toLowerCase();
          return nameA.localeCompare(nameB);
        });

        renderPriceList(priceListData);

      } catch (error) {
        console.error('❌ Error loading price list:', error);
        document.getElementById('priceListContainer').innerHTML = `
          <div class="empty-state">
            <i class="fas fa-exclamation-triangle"></i>
            <h3>Error Loading Price List</h3>
            <p>Error: ${error.message}</p>
            <button class="btn-primary" onclick="loadPriceList()"><i class="fas fa-sync"></i> Retry</button>
          </div>
        `;
      }
    }

    function renderPriceList(data) {
      const container = document.getElementById('priceListContainer');

      if (data.length === 0) {
        container.innerHTML = `
          <div class="empty-state">
            <i class="fas fa-tags"></i>
            <h3>No Items Found</h3>
            <p>No price list items available</p>
          </div>
        `;
        return;
      }

      // Create table
      const table = document.createElement('table');
      table.className = 'data-table';
      
      // Table header with checkbox for select all
      table.innerHTML = `
        <thead>
          <tr style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);">
            <th style="width: 50px;">
              <input type="checkbox" id="selectAllPriceItems" onchange="toggleSelectAllPriceItems(this.checked)">
            </th>
            <th>Item Number</th>
            <th>Item Name</th>
            <th>Description</th>
            <th>Unit Cost</th>
            <th>Margin (%)</th>
            <th>Sell Price</th>
            <th>Unit</th>
          </tr>
        </thead>
        <tbody id="priceListTableBody">
        </tbody>
      `;
      
      const tbody = table.querySelector('#priceListTableBody');
      
      data.forEach(item => {
        const unitCost = parseFloat(item.unit_cost) || 0;
        const margin = parseFloat(item.margin) || 0;
        const sellPrice = unitCost * (1 + margin / 100);
        
        const row = document.createElement('tr');
        row.innerHTML = `
          <td>
            <input type="checkbox" class="price-item-checkbox" value="${item.id}" data-item='${JSON.stringify(item).replace(/'/g, "&apos;")}'>
          </td>
          <td><strong>${item.item_number}</strong></td>
          <td>${item.item_name}</td>
          <td>${item.description || 'N/A'}</td>
          <td>$${unitCost.toFixed(2)}</td>
          <td>
            <span class="editable-margin" onclick="openMarginModal('${item.id}', '${item.item_name}', ${margin})" style="cursor: pointer; color: #667eea; text-decoration: underline;">
              ${margin.toFixed(1)}%
            </span>
          </td>
          <td><strong style="color: #10b981;">$${sellPrice.toFixed(2)}</strong></td>
          <td>${item.unit_of_measure || 'N/A'}</td>
        `;
        tbody.appendChild(row);
      });

      container.innerHTML = '';
      container.appendChild(table);
      
      // Update button states
      updatePriceListButtons();
    }
    
    function toggleSelectAllPriceItems(checked) {
      const checkboxes = document.querySelectorAll('.price-item-checkbox');
      checkboxes.forEach(cb => cb.checked = checked);
      updatePriceListButtons();
    }
    
    function updatePriceListButtons() {
      const selectedCount = document.querySelectorAll('.price-item-checkbox:checked').length;
      const downloadBtn = document.getElementById('downloadSelectedPDF');
      const emailBtn = document.getElementById('emailSelectedPDF');
      
      if (downloadBtn) {
        downloadBtn.disabled = selectedCount === 0;
        downloadBtn.textContent = selectedCount > 0 ? `Download PDF (${selectedCount} items)` : 'Download PDF';
      }
      if (emailBtn) {
        emailBtn.disabled = selectedCount === 0;
        emailBtn.textContent = selectedCount > 0 ? `Email PDF (${selectedCount} items)` : 'Email PDF';
      }
    }
    
    async function downloadSelectedPricePDF() {
      const selected = getSelectedPriceItems();
      if (selected.length === 0) {
        alert('Please select at least one item');
        return;
      }
      await generatePricePDF(selected, 'download');
    }
    
    async function emailSelectedPricePDF() {
      const selected = getSelectedPriceItems();
      if (selected.length === 0) {
        alert('Please select at least one item');
        return;
      }
      
      const email = prompt('Enter customer email address:');
      if (email) {
        await generatePricePDF(selected, 'email', email);
      }
    }
    
    async function downloadAllPricesPDF() {
      if (priceListData.length === 0) {
        alert('No items to export');
        return;
      }
      await generatePricePDF(priceListData, 'download');
    }
    
    function getSelectedPriceItems() {
      const checkboxes = document.querySelectorAll('.price-item-checkbox:checked');
      const items = [];
      checkboxes.forEach(cb => {
        try {
          const item = JSON.parse(cb.getAttribute('data-item').replace(/&apos;/g, "'"));
          items.push(item);
        } catch (e) {
          console.error('Error parsing item:', e);
        }
      });
      return items;
    }
    
    async function generatePricePDF(items, action, email) {
      // Simple PDF generation (in real app, use jsPDF or backend service)
      console.log('Generating PDF for', items.length, 'items');
      console.log('Action:', action);
      if (email) console.log('Email to:', email);
      
      // Create printable content
      let content = `
        <html>
        <head>
          <title>Price List - ${currentBusinessName}</title>
          <style>
            body { font-family: Arial, sans-serif; margin: 20px; }
            h1 { color: #667eea; }
            table { width: 100%; border-collapse: collapse; margin-top: 20px; }
            th, td { border: 1px solid #ddd; padding: 12px; text-align: left; }
            th { background: #667eea; color: white; }
            .total { font-weight: bold; background: #f3f4f6; }
          </style>
        </head>
        <body>
          <h1>${currentBusinessName}</h1>
          <h2>Price List</h2>
          <p>Date: ${new Date().toLocaleDateString()}</p>
          <table>
            <thead>
              <tr>
                <th>Item #</th>
                <th>Item Name</th>
                <th>Description</th>
                <th>Unit Cost</th>
                <th>Margin</th>
                <th>Sell Price</th>
                <th>Unit</th>
              </tr>
            </thead>
            <tbody>
      `;
      
      items.forEach(item => {
        const unitCost = parseFloat(item.unit_cost) || 0;
        const margin = parseFloat(item.margin) || 0;
        const sellPrice = unitCost * (1 + margin / 100);
        
        content += `
          <tr>
            <td>${item.item_number}</td>
            <td>${item.item_name}</td>
            <td>${item.description || 'N/A'}</td>
            <td>$${unitCost.toFixed(2)}</td>
            <td>${margin.toFixed(1)}%</td>
            <td>$${sellPrice.toFixed(2)}</td>
            <td>${item.unit_of_measure || 'N/A'}</td>
          </tr>
        `;
      });
      
      content += `
            </tbody>
          </table>
        </body>
        </html>
      `;
      
      if (action === 'download') {
        // Open in new window for printing/saving as PDF
        const printWindow = window.open('', '_blank');
        printWindow.document.write(content);
        printWindow.document.close();
        printWindow.print();
      } else if (action === 'email') {
        alert(`PDF would be emailed to: ${email}\n(In production, this would send via backend)`);
        // In production: send content to backend API to generate PDF and email
      }
    }
    // Auto-update unit_cost from latest inventory_history entry
    async function syncPriceListFromInventory() {
      if (!currentBusiness) {
        console.error('❌ No business loaded');
        return;
      }
      
      console.log('🔄 Syncing unit costs from inventory_history for client:', currentBusiness);
      
      try {
        // Get all inventory entries
        const inventorySnapshot = await db.collection('inventory_history')
          .where('client_id', '==', currentBusiness)
          .orderBy('posting_date', 'desc')
          .get();
        
        console.log('📦 Found', inventorySnapshot.size, 'inventory entries');
        
        // Group by item_number and get latest unit_cost for each
        const latestCosts = {};
        inventorySnapshot.forEach(doc => {
          const data = doc.data();
          const itemNum = data.item_number;
          
          if (itemNum && !latestCosts[itemNum]) {
            latestCosts[itemNum] = {
              unit_cost: data.unit_cost || 0,
              posting_date: data.posting_date
            };
            console.log(`📊 Latest cost for ${itemNum}: $${data.unit_cost}`);
          }
        });
        
        console.log('💰 Latest costs:', latestCosts);
        
        // Update price_list items with latest costs
        const priceSnapshot = await db.collection('price_list')
          .where('client_id', '==', currentBusiness)
          .get();
        
        console.log('💵 Found', priceSnapshot.size, 'price_list items');
        
        let updateCount = 0;
        const batch = db.batch();
        
        priceSnapshot.forEach(doc => {
          const priceItem = doc.data();
          const latestCost = latestCosts[priceItem.item_number];
          
          if (latestCost && latestCost.unit_cost !== priceItem.unit_cost) {
            batch.update(doc.ref, {
              unit_cost: latestCost.unit_cost,
              updated_at: firebase.firestore.FieldValue.serverTimestamp(),
              last_cost_sync: latestCost.posting_date
            });
            updateCount++;
            console.log(`📝 Updating ${priceItem.item_name}: $${priceItem.unit_cost} → $${latestCost.unit_cost}`);
          }
        });
        
        if (updateCount > 0) {
          await batch.commit();
          console.log(`✅ Updated ${updateCount} items with latest costs`);
          alert(`✅ Updated ${updateCount} items with latest costs from inventory`);
          // Reload price list to show updated values
          await loadPriceList();
        } else {
          console.log('✅ All costs are up to date');
          alert('✅ All costs are already up to date');
        }
        
      } catch (error) {
        console.error('❌ Error syncing costs:', error);
      }
    }
    function filterPriceList() {
      const searchTerm = document.getElementById('priceSearchInput').value.toLowerCase();
      
      const filtered = itemListData.filter(item => 
        item.item_name.toLowerCase().includes(searchTerm) ||
        (item.item_number && item.item_number.toLowerCase().includes(searchTerm)) ||
        (item.description && item.description.toLowerCase().includes(searchTerm))
      );

      renderPriceList(filtered);
    }

    function openAddPriceModal() {
      document.getElementById('priceModalTitle').innerHTML = '<i class="fas fa-tag"></i> Add Price Item';
      document.getElementById('priceForm').reset();
      document.getElementById('priceDocId').value = '';
      document.getElementById('priceModal').classList.add('active');
    }

    function editPriceItem(item) {
      document.getElementById('priceModalTitle').innerHTML = '<i class="fas fa-edit"></i> Edit Price Item';
      document.getElementById('priceDocId').value = item.id;
      document.getElementById('priceItemNumber').value = item.item_number;
      document.getElementById('priceItemName').value = item.item_name;
      document.getElementById('priceDescription').value = item.description || '';
      document.getElementById('priceUnitCost').value = item.unit_cost;
      document.getElementById('priceMargin').value = item.margin;
      document.getElementById('priceUnitOfMeasure').value = item.unit_of_measure;
      document.getElementById('priceModal').classList.add('active');
    }

    function closePriceModal() {
      document.getElementById('priceModal').classList.remove('active');
      document.getElementById('priceForm').reset();
    }

    document.getElementById('priceForm').addEventListener('submit', async (e) => {
      e.preventDefault();

      const docId = document.getElementById('priceDocId').value;
      const itemNumber = document.getElementById('priceItemNumber').value;
      const itemName = document.getElementById('priceItemName').value;
      const description = document.getElementById('priceDescription').value;
      const unitCost = parseFloat(document.getElementById('priceUnitCost').value);
      const margin = parseFloat(document.getElementById('priceMargin').value);
      const unitOfMeasure = document.getElementById('priceUnitOfMeasure').value;

      const priceData = {
        client_id: currentBusiness,
        client_name: currentBusinessName,
        item_number: itemNumber,
        item_name: itemName,
        description: description,
        unit_cost: unitCost,
        margin: margin,
        unit_of_measure: unitOfMeasure,
        updated_at: firebase.firestore.FieldValue.serverTimestamp()
      };

      try {
        if (docId) {
          await db.collection('price_list').doc(docId).update(priceData);
        } else {
          priceData.created_at = firebase.firestore.FieldValue.serverTimestamp();
          await db.collection('price_list').add(priceData);
        }

        closePriceModal();
        await loadItemList();
          await loadPriceList();
      } catch (error) {
        console.error('Error saving price item:', error);
        alert('Error: ' + error.message);
      }
    });

    async function deletePriceItem(id, itemName) {
      if (confirm(`Delete "${itemName}"?`)) {
        try {
          await db.collection('price_list').doc(id).delete();
          await loadItemList();
          await loadPriceList();
        } catch (error) {
          console.error('Error deleting:', error);
          alert('Error: ' + error.message);
        }
      }
    }

    // Quick Margin Edit
    function openMarginModal(itemId, itemName, currentMargin) {
      document.getElementById('marginItemId').value = itemId;
      document.getElementById('marginItemName').textContent = itemName;
      document.getElementById('marginValue').value = currentMargin;
      document.getElementById('marginModal').classList.add('active');
    }

    function closeMarginModal() {
      document.getElementById('marginModal').classList.remove('active');
      document.getElementById('marginForm').reset();
    }

    document.getElementById('marginForm').addEventListener('submit', async (e) => {
      e.preventDefault();

      const itemId = document.getElementById('marginItemId').value;
      const newMargin = parseFloat(document.getElementById('marginValue').value);

      try {
        await db.collection('price_list').doc(itemId).update({
          margin: newMargin,
          updated_at: firebase.firestore.FieldValue.serverTimestamp()
        });

        closeMarginModal();
        await loadItemList();
          await loadPriceList();
      } catch (error) {
        console.error('Error updating margin:', error);
        alert('Error: ' + error.message);
      }
    });

    // Responsive
    window.addEventListener('resize', () => {
    
    // Update price list button states when checkboxes change
    document.addEventListener('change', (e) => {
      if (e.target.classList.contains('price-item-checkbox')) {
        updatePriceListButtons();
      }
    });
      isMobile = window.innerWidth <= 768;
    });
  </script>

  <!-- SheetJS Library for Excel processing -->
  <script src="https://cdn.sheetjs.com/xlsx-0.20.1/package/dist/xlsx.full.min.js"></script>

</body>
</html>




<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Sampars Downtrade Ultra Modern</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<script src="https://cdn.tailwindcss.com"></script>
<script>
 tailwind.config = { theme: { extend: { fontFamily: { sans: ['Inter', 'sans-serif'], display: ['Plus Jakarta Sans', 'sans-serif'], }, colors: { brand: { 50: '#f0f7ff', 100: '#e0effe', 200: '#bae0fd', [...]
</script>
<style>
body { font-family: 'Inter', sans-serif; background-color: #f8fafc; color: #0f172a; }
.font-display { font-family: 'Plus Jakarta Sans', sans-serif; }
.glass-card { background: rgba(255, 255, 255, 0.92); backdrop-filter: blur(8px); border: 1px solid rgba(255, 255, 255, 0.6); box-shadow: 0 10px 30px -5px rgba(0, 0, 0, 0.04); }
/* Sidebar show/hide */
#sidebar { transform: translateX(-100%); transition: transform .32s cubic-bezier(.4,0,.2,1); z-index:1000; }
#sidebar.open { transform: translateX(0); }
#overlay { z-index: 900; transition: opacity .25s ease; opacity: 0; pointer-events: none; }
#overlay.show { opacity: 1; pointer-events: auto; }
.modern-input { background:#fff; border:1.5px solid #f1f5f9; transition: all .18s ease; }
.modern-input:focus { border-color:#2563eb; box-shadow:0 0 0 6px rgba(37,99,235,0.06); outline: none; }
.date-picker { background: white; border: 1px solid #e2e8f0; border-radius: .75rem; padding: .5rem; }
.fixed-top-action { position: sticky; top: 1rem; z-index: 30; background: transparent; }
.modal-backdrop { background: rgba(2,6,23,0.5); }
.popout { transition: transform .12s ease, box-shadow .12s ease; }
.popout:hover { transform: translateY(-3px); box-shadow: 0 8px 24px rgba(2,6,23,0.08); }
/* subtle editable target: small edit button */
.edit-target-btn { font-size: 12px; padding: 4px 6px; border-radius: 6px; border: 1px solid #e6e7eb; background: #fff; cursor: pointer; }
.segment { display:inline-flex; gap:6px; background:#fff; border-radius:999px; padding:4px; border:1px solid #e6e7eb; }
.segment button { padding:6px 10px; border-radius:999px; background:transparent; border: none; cursor: pointer; }
.segment button.active { background:#2563eb; color:white; }
.hide-scrollbar { scrollbar-width: none; -ms-overflow-style: none; }
.hide-scrollbar::-webkit-scrollbar { display: none; }
.badge-new { display:inline-flex; align-items:center; gap:6px; padding:4px 8px; background:#ecfdf5; color:#065f46; border-radius:999px; font-weight:600; font-size:12px; }
.badge-dot { width:8px; height:8px; background:#10b981; border-radius:999px; display:inline-block; }

/* runtime injected sticky CSS will be appended by script */
</style>
</head>
<body class="overflow-x-hidden">
<!-- Sidebar -->
<div id="sidebar" class="fixed top-0 left-0 w-[260px] h-full bg-white shadow-2xl border-r border-slate-100 flex flex-col">
  <div class="p-8 border-b border-slate-50">
    <div class="flex items-center gap-3">
      <div class="w-10 h-10 bg-brand-600 rounded-xl flex items-center justify-center shadow-lg shadow-brand-600/20">
        <span class="text-white font-black text-xl">D</span>
      </div>
      <div>
        <h1 class="font-display font-bold text-lg leading-tight text-slate-900">Sampars</h1>
        <span class="text-[10px] font-black uppercase tracking-widest text-slate-400">Sales Office</span>
      </div>
    </div>
  </div>
  <nav class="flex-1 p-4 space-y-2 mt-4">
    <button onclick="showHome()" class="w-full flex items-center gap-4 px-4 py-3 rounded-2xl text-sm font-semibold text-slate-600 hover:bg-slate-50 hover:text-brand-600 transition-all group"> <span cl[...]
    <button onclick="showCustomers()" class="w-full flex items-center gap-4 px-4 py-3 rounded-2xl text-sm font-semibold text-slate-600 hover:bg-slate-50 hover:text-brand-600 transition-all group"> <sp[...]
    <button onclick="showPriceList()" class="w-full flex items-center gap-4 px-4 py-3 rounded-2xl text-sm font-semibold text-slate-600 hover:bg-slate-50 hover:text-brand-600 transition-all group"> <sp[...]
    <button onclick="showPriceSurvey()" class="w-full flex items-center gap-4 px-4 py-3 rounded-2xl text-sm font-semibold text-slate-600 hover:bg-slate-50 hover:text-brand-600 transition-all group"> <[...]
    <button onclick="showPriceSurveyFeedback()" class="w-full flex items-center gap-4 px-4 py-3 rounded-2xl text-sm font-semibold text-slate-600 hover:bg-slate-50 hover:text-brand-600 transition-all g[...]
    <button onclick="showSalesDashboard()" class="w-full flex items-center gap-4 px-4 py-3 rounded-2xl text-sm font-semibold text-slate-600 hover:bg-slate-50 hover:text-brand-600 transition-all group"[...]
  </nav>
  <div class="p-6 mt-auto border-t border-slate-50 bg-slate-50/50">
    <div class="flex items-center gap-3">
      <div class="w-10 h-10 rounded-full bg-brand-100 border-2 border-white flex items-center justify-center text-brand-700 font-bold text-xs shadow-sm">MGD</div>
      <div class="text-xs">
        <p class="font-bold text-slate-800">Sampars</p>
        <p class="text-slate-500">Marcus Garvey</p>
      </div>
    </div>
  </div>
</div>
<!-- Overlay -->
<div id="overlay" class="fixed inset-0 bg-slate-900/20 backdrop-blur-sm hidden" onclick="hideSidebar()"></div>
<!-- Top Navigation -->
<header class="sticky top-0 z-40 bg-white/70 backdrop-blur-md border-b border-slate-100 px-6 py-4">
  <div class="max-w-7xl mx-auto flex items-center justify-between">
    <div class="flex items-center gap-4">
      <button id="menuBtn" onclick="toggleMenu()" class="w-10 h-10 rounded-xl hover:bg-slate-100 flex items-center justify-center transition-colors">
        <svg class="w-6 h-6 text-slate-600" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></pa[...]
      </button>
      <h2 id="pageTitle" class="font-display font-extrabold text-xl text-slate-900 tracking-tight">Deal of the Day</h2>
    </div>
    <div class="flex items-center gap-3">
      <span class="hidden md:inline-flex text-[10px] font-black bg-brand-50 text-brand-600 px-2.5 py-1 rounded-lg uppercase tracking-widest">System Operational</span>
      <div class="w-8 h-8 rounded-full bg-slate-100 border border-slate-200"></div>
    </div>
  </div>
</header>

<!-- Add Customer Modal -->
<div id="addCustomerModal" class="fixed inset-0 hidden items-center justify-center modal-backdrop z-50">
  <div class="bg-white rounded-lg w-full max-w-2xl p-6 shadow-xl">
    <div class="flex justify-between items-center mb-4">
      <h3 class="font-bold text-lg">Add New Customer</h3>
      <button onclick="closeAddModal()" class="text-slate-500 hover:text-slate-800">✕</button>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
      <input id="modal_salesCode" placeholder="Sales Code" class="modern-input p-3 rounded" />
      <input id="modal_salesRep" placeholder="Sales Rep Name" class="modern-input p-3 rounded" />
      <input id="modal_businessName" placeholder="Business Name" class="modern-input p-3 rounded" />
      <input id="modal_customerNumber" placeholder="Customer Number" class="modern-input p-3 rounded" />
      <input id="modal_businessType" placeholder="Business Type" class="modern-input p-3 rounded" />
      <input id="modal_customerName" placeholder="Customer Name" class="modern-input p-3 rounded" />
      <input id="modal_address" placeholder="Address" class="modern-input p-3 rounded md:col-span-2" />
    </div>
    <div class="mt-4 flex justify-end gap-2">
      <button onclick="closeAddModal()" class="px-4 py-2 rounded border">Cancel</button>
      <button onclick="modalSubmitNewCustomer()" class="px-4 py-2 rounded bg-brand-600 text-white">Add Customer</button>
    </div>
  </div>
</div>

<main id="content" class="content max-w-7xl mx-auto py-10 px-6 animate-slide-up"></main>

<script>
/* Full script (V1 base) with only the Deal of the Day and Price List changed to V6 behavior.
   Everything else remains the same as V1. */

/* Globals & helpers */
let sidebarOpen = false;
const sidebarEl = document.getElementById('sidebar');
const overlayEl = document.getElementById('overlay');
function toggleMenu(){ sidebarOpen = !sidebarOpen; if (sidebarOpen){ sidebarEl.classList.add('open'); overlayEl.classList.add('show'); overlayEl.classList.remove('hidden'); } else { sidebarEl.classLis[...]
function hideSidebar(){ sidebarOpen=false; sidebarEl.classList.remove('open'); overlayEl.classList.remove('show'); overlayEl.classList.add('hidden'); }
function setPageTitle(t){ document.getElementById('pageTitle').innerText = t; }
function escapeHtml(s){ if (s===null||s===undefined) return ''; return String(s).replace(/[&<>"']/g, function(m){ return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m]; }); }
function idify(s){ return String(s).replace(/[^a-zA-Z0-9-_]/g,'_'); }
function formatMoney(n){ if (n===null||n===undefined||n==='') return '—'; const num=Number(n); if (isNaN(num)) return String(n); return '$' + num.toLocaleString(undefined,{minimumFractionDigits:2,ma[...]
function formatDateLongTime(v){ if (!v) return ''; const d=new Date(v); if (isNaN(d.getTime())) return String(v); const opts={year:'numeric',month:'long',day:'numeric',hour:'numeric',minute:'2-digit'}[...]

/* Inject sticky CSS for price table header + first two columns */
(function(){ const css = `.price-table thead th{ position:sticky; top:0; background:#fff; z-index:4;} .price-table tbody td.sticky-col-0, .price-table thead th.sticky-col-0{ position:sticky; left:0; z[...]

/* ========================= Home / Deal of the Day (V6-style update applied to V1 base) ========================= */
function showHome(){ hideSidebar(); setPageTitle("Deal of the Day"); content.innerHTML = ` <div class="grid gap-8 md:grid-cols-12"> <div class="md:col-span-12 glass-card rounded-3xl p-8 border border-[...]
function renderDealPosts(posts){ const el=document.getElementById('deal'); if(!posts||posts.length===0){ el.innerHTML='<div class="p-6 text-slate-400">No broadcast posts</div>'; return; } let html='';[...]
function saveHomeDeal(){ const val=document.getElementById('dealInput').value; if(!val){ alert('Please enter a message.'); return; } const pw=prompt('Enter password to add broadcast:'); if(pw===null) [...]
function deleteDealPrompt(index){ const pw=prompt('Enter password to delete this post:'); if(pw===null) return; if(window.google && google.script && google.script.run){ google.script.run.withSuccessHa[...]

/* ========================= Customers (unchanged V1) ========================= */
const CUSTOMER_FIELDS = [ {title: 'Sales Code', synonyms: ['sales code','salescode','sales_code']}, {title: 'Sales Rep Name', synonyms: ['sales rep name','sales rep','salesrep','sales_rep_name']}, {ti[...]
function normalizeHeader(h){ if(h===null||h===undefined) return ''; return String(h).toLowerCase().replace(/[\.\#\$\[\]]/g,'').replace(/\s+/g,' ').trim(); }
function showCustomers(){ hideSidebar(); setPageTitle("Customer Lookup"); content.innerHTML = ` <div class="glass-card rounded-3xl overflow-hidden border border-slate-100 p-6"> <div class="flex justif[...]
let windowCustomerData = [];
function refreshCustomers(){ if(window.google && google.script && google.script.run){ google.script.run.withSuccessHandler(function(data){ windowCustomerData=data||[]; renderCustomersGrid(windowCustom[...]
function resetCustomers(){ document.getElementById('customerSearch').value=''; refreshCustomers(); }
function renderCustomersGrid(data){ const grid=document.getElementById('customersGrid'); if(!data||data.length<=1){ grid.innerHTML=`<div class="p-20 text-center text-slate-400 font-medium">No customer[...]

/* ========================= Price List (V6 changes applied to V1) ========================= */
function showPriceList(){ hideSidebar(); setPageTitle("Price List"); content.innerHTML = ` <div class="glass-card rounded-3xl overflow-hidden border border-slate-100"> <div class="p-8 border-b border-[...]

let fullPriceData = [];
let displayedPriceData = [];

function refreshPriceList(){
  if (window.google && google.script && google.script.run) {
    google.script.run.withSuccessHandler(function(data){
      fullPriceData = data || [];
      displayedPriceData = fullPriceData.slice();
      renderPriceList(displayedPriceData);
    }).withFailureHandler(function(err){
      console.error('getPriceList failed', err);
      document.getElementById('priceTable').innerHTML = '<div class="p-6 text-red-500">Failed to load price list</div>';
    }).getPriceList();
  } else {
    fullPriceData = [["Groceries","White Rice",35.00,"bag","Bulk",30.00,"In-Stock","Admin",new Date().toISOString()]];
    displayedPriceData = fullPriceData.slice();
    renderPriceList(displayedPriceData);
  }
}
function resetPriceList(){ document.getElementById('priceSearchInput').value=''; displayedPriceData = fullPriceData.slice(); renderPriceList(displayedPriceData); }

function renderPriceList(data) {
  try {
    const tableDiv = document.getElementById("priceTable");
    if (!data || data.length === 0) { tableDiv.innerHTML = `<div class="p-6 text-slate-400">No price data</div>`; return; }
    var recentCount = 0; var now=new Date();
    for(var i=0;i<data.length;i++){ var u=data[i][8]; if(u){ var ud=(typeof u==='string')?new Date(u):new Date(u); if(!isNaN(ud.getTime())){ var diff=(now-ud)/(1000*60*60*24); if(diff<=7) recentCount+[...]
    document.getElementById('pricePreview').innerHTML = recentCount>0?(`<span class="badge-new"><span class="badge-dot"></span> ${recentCount} New!</span>`):`<span class="text-slate-400">No recent upd[...]

    let html = `<div class="overflow-x-auto"><table class="w-full text-left text-sm price-table"><thead class="bg-slate-50"><tr> <th class="px-4 py-2 sticky-col-0">Category</th> <th class="px-4 py-2 s[...]
    data.forEach((r,i) => {
      const origVal = (r[2]!==undefined&&r[2]!==null&&r[2]!=='')?Number(r[2]):'';
      const dealVal = (r[5]!==undefined&&r[5]!==null&&r[5]!=='')?Number(r[5]):'';
      let recentBadge='';
      const updatedRaw=r[8];
      if(updatedRaw){ const ud=(typeof updatedRaw==='string')?new Date(updatedRaw):new Date(updatedRaw); if(!isNaN(ud.getTime())){ var diffDays=(new Date()-ud)/(1000*60*60*24); if(diffDays<=7) recentB[...]
      html+=`<tr class="border-b"> <td class="px-4 py-2 sticky-col-0">${escapeHtml(r[0]||'')}</td> <td class="px-4 py-2 font-bold sticky-col-1">${escapeHtml(r[1]||'')}</td> <td class="px-4 py-2 text-r[...]
    });
    html += `</tbody></table></div>`;
    tableDiv.innerHTML = html;
  } catch(e){ console.error('renderPriceList failed', e); document.getElementById('priceTable').innerHTML = '<div class="p-6 text-red-500">Error rendering price list (see console)</div>'; }
}

function filterPriceList(){ const searchVal=document.getElementById("priceSearchInput")?.value?.toLowerCase()||""; if(!searchVal){ displayedPriceData=fullPriceData.slice(); renderPriceList(displayedPr[...]

/* Inline edit original price */
function enterEditPrice(i,currentValue){ const displayEl=document.getElementById('orig_display_'+i); if(!displayEl) return; const inputId='orig_input_'+i; const saveBtnId='orig_save_'+i; const cancelB[...]

/* Save changes (bulk) */
function savePriceChanges(){ const pw=prompt('Enter password to save price changes:'); if(pw===null) return; if(!(window.google && google.script && google.script.run)){ alert('Mock save - no Apps Scri[...]

/* ----------------- PDF generation & Custom Popout (V6 behavior applied) ----------------- */
function generateFullPricePDF(){ if(!(window.google && google.script && google.script.run)){ alert('Mock generate PDF'); return; } google.script.run.withSuccessHandler(downloadBase64).withFailureHandl[...]

function openCustomPriceModal(){ const modal=document.getElementById('customPriceModal'); document.getElementById('customSearchInput').value=''; document.getElementById('customEmail').value=''; docume[...]
function closeCustomPriceModal(){ const modal=document.getElementById('customPriceModal'); modal.classList.remove('flex'); modal.classList.add('hidden'); const sug=document.getElementById('custom_sugg[...]
function addProductFromSearch(){ const q=(document.getElementById('customSearchInput')?.value||'').trim(); if(!q) return alert('Type to search and pick a product from suggestions.'); const found=(wind[...]
function addProductByIndex(idx){ window._selectedCustom = window._selectedCustom || []; if(window._selectedCustom.some(s=>s.idx===idx)) return; const row = fullPriceData[idx]||[]; const priceVal = (ro[...]
function renderCustomSelected(){ const cont=document.getElementById('customSelectedList'); const items=window._selectedCustom||[]; if(!items.length){ cont.innerHTML='<div class="p-4 text-slate-400">No[...]
function removeCustomItem(i){ (window._selectedCustom||[]).splice(i,1); renderCustomSelected(); }

function generateCustomPricePDF(sendEmail){ const selected=(window._selectedCustom||[]).map(it=>({ category: fullPriceData[it.idx][0]||'', product: it.product, price: (it.price !== undefined && it.pri[...]

/* Utility to download base64 */
function downloadBase64(obj){ if(!obj||!obj.data){ alert('No data returned'); return; } const b64=obj.data; const byteChars=atob(b64); const byteNumbers=new Array(byteChars.length); for(let i=0;i<byte[...]

/* ========================= Price Survey, Feedback, Sales Dashboard (V1 kept) ========================= */
/* (All V1 logic left unchanged for survey and sales dashboard functions.) */
function showPriceSurvey(){ hideSidebar(); setPageTitle('Price Survey'); content.innerHTML = ` <div class="glass-card rounded-3xl p-6"> <h2 class="font-bold text-lg">Price Survey</h2> <p class="text-s[...]
function submitSurvey(){ const entry={ itemName: document.getElementById('survey_item')?.value, unit: document.getElementById('survey_unit')?.value, supplier: document.getElementById('survey_supplier'[...]

function showPriceSurveyFeedback(){ hideSidebar(); setPageTitle('Price Survey Feedback'); content.innerHTML = ` <div class="glass-card rounded-3xl p-6"> <div class="flex justify-between items-center">[...]
let windowSurveyData=[]; function refreshSurveyFeedback(){ if(!(window.google && google.script && google.script.run)){ windowSurveyData=[['admin@','2026-01-01','ACME','White Rice','bag',35,'Sample']];[...]
function renderSurveyFeedback(data){ const c=document.getElementById('surveyList'); if(!data||data.length===0){ c.innerHTML='<div class="p-6 text-slate-500">No responses</div>'; return; } let html='<d[...]
function filterSurveyFeedback(){ const q=(document.getElementById('survey_filter')?.value||'').toLowerCase().trim(); if(!windowSurveyData) return; if(!q){ renderSurveyFeedback(windowSurveyData); retur[...]

/* ========================= Sales Dashboard (restored from V1) ========================= */
let windowSalesData = []; let windowRawCashData=[]; let windowRawCreditData=[]; let rawView='cash';
function showSalesDashboard(){
  hideSidebar(); setPageTitle("Sales Performance");
  content.innerHTML = `
  <div class="grid gap-6 mb-8 md:grid-cols-5">
    <div class="glass-card p-6 rounded-3xl border border-white">
      <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-1">Dept Target</p>
      <h4 id="statDeptTarget" class="text-2xl font-display font-bold text-slate-900">$0.00</h4>
    </div>
    <div class="glass-card p-6 rounded-3xl border border-white">
      <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-1">Total Sales</p>
      <h4 id="statTotalSales" class="text-2xl font-display font-bold text-slate-900">$0.00</h4>
    </div>
    <div class="glass-card p-6 rounded-3xl border border-white">
      <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-1">Avg Performance</p>
      <h4 id="statAvgPerf" class="text-2xl font-display font-bold text-emerald-500">0%</h4>
    </div>
    <div class="glass-card p-6 rounded-3xl border border-white">
      <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-1">Cash vs Credit</p>
      <h4 id="statCashCredit" class="text-2xl font-display font-bold text-slate-900">0/0</h4>
    </div>
    <div class="glass-card p-6 rounded-3xl border border-white">
      <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-1">Customer Reach</p>
      <h4 id="statCustReach" class="text-2xl font-display font-bold text-brand-600">0%</h4>
    </div>
  </div>

  <div class="glass-card rounded-3xl overflow-hidden border border-slate-100 mb-8">
    <div class="p-8 border-b border-slate-50 flex justify-between items-center">
      <div>
        <h3 class="font-display font-bold text-lg text-slate-900">Sales Breakdown</h3>
        <p class="text-sm text-slate-500 font-medium">Representative performance tracking against targets.</p>
      </div>
    </div>
    <div id="salesTable" class="overflow-x-auto p-4">
      <div class="p-6 text-slate-500">Loading Sales Data...</div>
    </div>
  </div>

  <div class="glass-card rounded-3xl p-8 border border-slate-100 mb-8">
    <h3 class="font-display font-bold text-lg text-slate-900 mb-4">Top 3 Performers (Closest to Target %)</h3>
    <div id="topPerformers" class="overflow-x-auto">
      <div class="p-10 text-center"><span class="animate-pulse font-bold text-slate-300">Loading Top Performers...</span></div>
    </div>
  </div>

  <div class="glass-card rounded-3xl overflow-hidden border border-slate-100">
    <div class="p-8 border-b border-slate-50 flex justify-between items-center">
      <div>
        <h3 class="font-display font-bold text-lg text-slate-900">Raw Sales Breakdown</h3>
        <p class="text-sm text-slate-500 font-medium">Detailed transaction data from Cash and Credit sales.</p>
      </div>
      <div>
        <div class="segment">
          <button id="seg_cash" class="active" onclick="setRawView('cash')">Cash Sales</button>
          <button id="seg_credit" onclick="setRawView('credit')">Credit Sales</button>
        </div>
      </div>
    </div>
    <div class="px-4 pb-4">
      <div id="rawControls" class="flex flex-col sm:flex-row gap-4 mb-6 mt-4"></div>
      <div class="flex justify-end gap-2 mb-2">
        <button onclick="downloadRaw('cash')" class="px-3 py-2 rounded border">Download Cash CSV</button>
        <button onclick="downloadRaw('credit')" class="px-3 py-2 rounded border">Download Credit CSV</button>
      </div>
      <div id="rawContainer" class="mt-2">
        <div id="rawTableArea" class="overflow-x-auto p-2">
          <div class="p-6 text-slate-500">Select Cash or Credit to load raw data.</div>
        </div>
      </div>
    </div>
  </div>
  `;
  if (window.google && google.script && google.script.run) {
    google.script.run.withSuccessHandler(function(d){ windowSalesData = d || []; renderSalesData(windowSalesData); }).getSalesData();
    google.script.run.withSuccessHandler(function(d){ windowRawCashData = d || []; }).getCashSalesRaw();
    google.script.run.withSuccessHandler(function(d){ windowRawCreditData = d || []; }).getCreditSalesRaw();
  } else {
    windowSalesData = [ ["REP001", "James Smith", 100000, 45000, 50000, 95000, 0.95, 50, 45, 0.90, 200], ["REP002", "Sarah Wilson", 120000, 80000, 50000, 130000, 1.08, 60, 58, 0.96, 250] ];
    windowRawCashData = [["TXN001","STAFF001","CUST001","2024-01-01",100.00,5.00],["TXN002","STAFF002","CUST002","2024-01-05",200.00,10.00]];
    windowRawCreditData = [["1","CUST001","John Doe","2024-01-02",150.00],["2","CUST002","Jane Roe","2024-01-08",300.00]];
    renderSalesData(windowSalesData);
  }
  setRawView(rawView);
}

function renderSalesData(data) {
  const tableDiv = document.getElementById("salesTable");
  if (!data || data.length === 0) { tableDiv.innerHTML = `<div class="p-6 text-slate-500">No sales data available.</div>`; return; }
  let totalSalesSum = 0, totalPerfSum = 0, totalTargetSum = 0, cashSum = 0, creditSum = 0, custReachSum = 0;
  let html = `<div class="overflow-x-auto"><table class="w-full text-left text-xs"><thead class="bg-slate-50"><tr> <th class="px-6 py-4 text-[9px] font-black uppercase tracking-widest text-slate-400 b[...]
  data.forEach(function(r){
    const repId = r[0]; const name = r[1]; const target = parseFloat(r[2] || 0); const cash = parseFloat(r[3] || 0); const credit = parseFloat(r[4] || 0); const total = parseFloat(r[5] || 0); const sa[...]
    totalSalesSum += total; totalPerfSum += salesPerc; totalTargetSum += target; cashSum += cash; creditSum += credit; custReachSum += (isNaN(custPerc)?0:custPerc);
    const safeId = idify(repId);
    html += `<tr class="hover:bg-slate-50/50 transition-colors"> <td class="px-6 py-4"> <div class="font-bold text-slate-800">${escapeHtml(name)}</div> <div class="text-[10px] font-medium text-slate-4[...]
  });
  html += `</tbody></table></div>`;
  tableDiv.innerHTML = html;
  document.getElementById("statDeptTarget").innerText = formatMoney(totalTargetSum);
  document.getElementById("statTotalSales").innerText = formatMoney(totalSalesSum);
  document.getElementById("statAvgPerf").innerText = (totalPerfSum / data.length).toFixed(1) + "%";
  document.getElementById("statCashCredit").innerText = ((cashSum / 1000).toFixed(0) + "k / " + (creditSum / 1000).toFixed(0) + "k");
  document.getElementById("statCustReach").innerText = (custReachSum / data.length).toFixed(1) + "%";

  // top performers
  const sortedData = [...data].sort((a,b) => (parseFloat(b[6])||0) - (parseFloat(a[6])||0));
  const top3 = sortedData.slice(0,3);
  let topHtml = `<div class="space-y-4">`;
  top3.forEach(r=>{ const name=r[1]; const salesPerc=(parseFloat(r[6])||0)*100; const total=parseFloat(r[5]||0); const target=parseFloat(r[2]||0); topHtml += `<div class="flex justify-between items-ce[...]
  if(top3.length===0) topHtml += `<div class="text-center text-slate-400 py-4">Need more data for top 3</div>`;
  topHtml += `</div>`;
  document.getElementById("topPerformers").innerHTML = topHtml;
}

/* edit target UX */
function enterEditTarget(safeId, repIdDisplay, currentValue){
  const displayEl = document.getElementById('target_display_' + safeId);
  if (!displayEl) return;
  const inputId = 'target_input_' + safeId; const saveBtnId = 'target_save_' + safeId; const cancelBtnId = 'target_cancel_' + safeId;
  const html = `<input id="${inputId}" type="number" class="modern-input p-1 text-right w-28 inline-block" value="${currentValue}" /> <button id="${saveBtnId}" class="ml-2 edit-target-btn">Save</butto[...]
  displayEl.insertAdjacentHTML('afterend', html); displayEl.style.display='none';
  document.getElementById(saveBtnId).onclick=function(){ const newVal=Number(document.getElementById(inputId).value); if(isNaN(newVal)){ alert('Enter a valid number'); return; } const pw=prompt('Enter[...]
  document.getElementById(cancelBtnId).onclick=function(){ cleanup(); };
  function cleanup(){ const inp=document.getElementById(inputId); const s=document.getElementById(saveBtnId); const c=document.getElementById(cancelBtnId); if(inp) inp.remove(); if(s) s.remove(); if(c[...]
}

/* Raw view controls & renderers */
function setRawView(which){ rawView = which==='credit'? 'credit':'cash'; document.getElementById('seg_cash').classList.toggle('active', rawView==='cash'); document.getElementById('seg_credit').classLi[...]
function renderRawTable(type){ const tableArea=document.getElementById('rawTableArea'); if(type==='cash'){ const data=windowRawCashData||[]; if(!data.length){ tableArea.innerHTML='<div class="p-4 text[...]
function filterRawData(type){ if(type==='cash'){ const start=document.getElementById('cash_start')?.value; const end=document.getElementById('cash_end')?.value; const q=(document.getElementById('cash_[...]
function downloadRaw(type){ if(!(window.google && google.script && google.script.run)){ alert('Mock download'); return; } google.script.run.withSuccessHandler(function(obj){ if(!obj||!obj.data){ alert[...]

/* Initial route */
showHome();

// click outside sidebar to close
document.addEventListener('click', (e) => { if (!sidebarOpen) return; const sb=document.getElementById('sidebar'); const btn=document.getElementById('menuBtn'); if(!sb.contains(e.target) && !btn.conta[...]
</script>
</body>
</html>

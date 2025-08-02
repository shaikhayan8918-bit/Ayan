<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prospect Follow-up App</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 12px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }

        .header p {
            opacity: 0.9;
            font-size: 1.1rem;
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            padding: 30px;
        }

        .section {
            background: #f8f9fa;
            border-radius: 8px;
            padding: 25px;
            border: 1px solid #e9ecef;
        }

        .section h2 {
            color: #495057;
            margin-bottom: 20px;
            font-size: 1.4rem;
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
            color: #495057;
        }

        input, textarea, select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e9ecef;
            border-radius: 6px;
            font-size: 14px;
            transition: border-color 0.3s;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: #667eea;
        }

        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 6px;
            font-size: 14px;
            font-weight: 500;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .btn:hover {
            transform: translateY(-2px);
        }

        .btn-danger {
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
        }

        .prospects-list {
            max-height: 400px;
            overflow-y: auto;
        }

        .prospect-card {
            background: white;
            border: 1px solid #e9ecef;
            border-radius: 6px;
            padding: 15px;
            margin-bottom: 10px;
            transition: transform 0.2s;
        }

        .prospect-card:hover {
            transform: translateY(-1px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }

        .prospect-header {
            display: flex;
            justify-content: between;
            align-items: center;
            margin-bottom: 10px;
        }

        .prospect-email {
            font-weight: 600;
            color: #495057;
        }

        .prospect-company {
            color: #6c757d;
            font-size: 0.9rem;
        }

        .prospect-status {
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 0.8rem;
            font-weight: 500;
        }

        .status-pending {
            background: #fff3cd;
            color: #856404;
        }

        .status-sent {
            background: #d1ecf1;
            color: #0c5460;
        }

        .status-followup {
            background: #d4edda;
            color: #155724;
        }

        .next-followup {
            font-size: 0.85rem;
            color: #6c757d;
            margin-top: 5px;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
            border: 1px solid #e9ecef;
        }

        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            color: #667eea;
        }

        .stat-label {
            color: #6c757d;
            font-size: 0.9rem;
        }

        .email-template {
            margin-top: 20px;
        }

        .template-preview {
            background: #f8f9fa;
            border: 1px solid #e9ecef;
            border-radius: 4px;
            padding: 15px;
            margin-top: 10px;
            font-family: monospace;
            font-size: 0.9rem;
        }

        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .stats {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🚀 Prospect Follow-up</h1>
            <p>Automate your outreach and never miss a follow-up again</p>
        </div>

        <div class="stats">
            <div class="stat-card">
                <div class="stat-number" id="totalProspects">0</div>
                <div class="stat-label">Total Prospects</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="pendingFollowups">0</div>
                <div class="stat-label">Pending Follow-ups</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="sentToday">0</div>
                <div class="stat-label">Sent Today</div>
            </div>
        </div>

        <div class="main-content">
            <div class="section">
                <h2>📝 Add New Prospect</h2>
                <form id="prospectForm">
                    <div class="form-group">
                        <label for="email">Email Address</label>
                        <input type="email" id="email" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="firstName">First Name</label>
                        <input type="text" id="firstName" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="company">Company</label>
                        <input type="text" id="company">
                    </div>
                    
                    <div class="form-group">
                        <label for="followupDays">Follow-up After (days)</label>
                        <select id="followupDays">
                            <option value="5">5 days</option>
                            <option value="3">3 days</option>
                            <option value="7">7 days</option>
                            <option value="14">14 days</option>
                        </select>
                    </div>
                    
                    <button type="submit" class="btn">Add Prospect</button>
                </form>

                <div class="email-template">
                    <h3>Follow-up Template</h3>
                    <textarea id="emailTemplate" rows="6" placeholder="Hi {firstName},

I wanted to follow up on my previous email about...

Best regards,
Your Name">Hi {firstName},

I wanted to follow up on my previous email about our conversation regarding {company}.

Just checking if you had a chance to review the proposal I sent over. I'd love to answer any questions you might have.

Would you be available for a quick 15-minute call this week?

Best regards,
Your Name</textarea>
                </div>
            </div>

            <div class="section">
                <h2>📋 Your Prospects</h2>
                <div class="prospects-list" id="prospectsList">
                    <p style="text-align: center; color: #6c757d; padding: 40px;">
                        No prospects added yet. Add your first prospect to get started!
                    </p>
                </div>
            </div>
        </div>
    </div>

    <script>
        class ProspectManager {
            constructor() {
                this.prospects = JSON.parse(localStorage.getItem('prospects') || '[]');
                this.emailTemplate = localStorage.getItem('emailTemplate') || '';
                this.init();
            }

            init() {
                this.renderProspects();
                this.updateStats();
                this.loadTemplate();
                this.setupEventListeners();
                this.checkFollowups();
            }

            setupEventListeners() {
                document.getElementById('prospectForm').addEventListener('submit', (e) => {
                    e.preventDefault();
                    this.addProspect();
                });

                document.getElementById('emailTemplate').addEventListener('input', (e) => {
                    this.saveTemplate(e.target.value);
                });
            }

            addProspect() {
                const email = document.getElementById('email').value;
                const firstName = document.getElementById('firstName').value;
                const company = document.getElementById('company').value;
                const followupDays = parseInt(document.getElementById('followupDays').value);

                // Check if prospect already exists
                if (this.prospects.find(p => p.email === email)) {
                    alert('Prospect with this email already exists!');
                    return;
                }

                const prospect = {
                    id: Date.now(),
                    email,
                    firstName,
                    company,
                    followupDays,
                    dateAdded: new Date().toISOString(),
                    status: 'pending',
                    nextFollowup: this.calculateNextFollowup(followupDays),
                    followupsSent: 0
                };

                this.prospects.push(prospect);
                this.saveProspects();
                this.renderProspects();
                this.updateStats();
                
                // Clear form
                document.getElementById('prospectForm').reset();
                
                // Show success message
                this.showNotification('Prospect added successfully!');
            }

            calculateNextFollowup(days) {
                const date = new Date();
                date.setDate(date.getDate() + days);
                return date.toISOString();
            }

            renderProspects() {
                const container = document.getElementById('prospectsList');
                
                if (this.prospects.length === 0) {
                    container.innerHTML = `
                        <p style="text-align: center; color: #6c757d; padding: 40px;">
                            No prospects added yet. Add your first prospect to get started!
                        </p>
                    `;
                    return;
                }

                // Sort by next followup date
                const sortedProspects = [...this.prospects].sort((a, b) => 
                    new Date(a.nextFollowup) - new Date(b.nextFollowup)
                );

                container.innerHTML = sortedProspects.map(prospect => {
                    const nextFollowup = new Date(prospect.nextFollowup);
                    const isOverdue = nextFollowup < new Date();
                    const daysUntil = Math.ceil((nextFollowup - new Date()) / (1000 * 60 * 60 * 24));
                    
                    return `
                        <div class="prospect-card">
                            <div class="prospect-header">
                                <div>
                                    <div class="prospect-email">${prospect.email}</div>
                                    <div class="prospect-company">${prospect.company || 'No company'}</div>
                                </div>
                                <div>
                                    <span class="prospect-status status-${prospect.status}">${prospect.status}</span>
                                    <button class="btn btn-danger" onclick="app.removeProspect(${prospect.id})" style="margin-left: 10px; padding: 5px 10px; font-size: 12px;">Remove</button>
                                </div>
                            </div>
                            <div class="next-followup">
                                Next follow-up: ${nextFollowup.toLocaleDateString()} 
                                ${isOverdue ? '(OVERDUE!)' : `(${daysUntil} days)`}
                                ${prospect.followupsSent > 0 ? `• ${prospect.followupsSent} follow-ups sent` : ''}
                            </div>
                            ${isOverdue ? `<button class="btn" onclick="app.sendFollowup(${prospect.id})" style="margin-top: 10px;">Send Follow-up Now</button>` : ''}
                        </div>
                    `;
                }).join('');
            }

            sendFollowup(prospectId) {
                const prospect = this.prospects.find(p => p.id === prospectId);
                if (!prospect) return;

                // In a real app, this would actually send an email
                // For now, we'll simulate it
                const template = document.getElementById('emailTemplate').value;
                const personalizedEmail = template
                    .replace(/{firstName}/g, prospect.firstName)
                    .replace(/{company}/g, prospect.company || 'your company');

                console.log('Sending email to:', prospect.email);
                console.log('Email content:', personalizedEmail);

                // Update prospect
                prospect.followupsSent++;
                prospect.status = 'followup';
                prospect.nextFollowup = this.calculateNextFollowup(prospect.followupDays);
                
                this.saveProspects();
                this.renderProspects();
                this.updateStats();
                
                this.showNotification(`Follow-up sent to ${prospect.firstName}!`);
            }

            removeProspect(prospectId) {
                if (confirm('Are you sure you want to remove this prospect?')) {
                    this.prospects = this.prospects.filter(p => p.id !== prospectId);
                    this.saveProspects();
                    this.renderProspects();
                    this.updateStats();
                }
            }

            updateStats() {
                const total = this.prospects.length;
                const pending = this.prospects.filter(p => new Date(p.nextFollowup) < new Date()).length;
                const sentToday = this.prospects.filter(p => {
                    const today = new Date().toDateString();
                    return new Date(p.nextFollowup).toDateString() === today && p.status === 'followup';
                }).length;

                document.getElementById('totalProspects').textContent = total;
                document.getElementById('pendingFollowups').textContent = pending;
                document.getElementById('sentToday').textContent = sentToday;
            }

            checkFollowups() {
                // Check every hour for follow-ups that need to be sent
                setInterval(() => {
                    this.renderProspects();
                    this.updateStats();
                }, 60000); // Check every minute for demo purposes
            }

            saveProspects() {
                localStorage.setItem('prospects', JSON.stringify(this.prospects));
            }

            saveTemplate(template) {
                localStorage.setItem('emailTemplate', template);
            }

            loadTemplate() {
                const template = localStorage.getItem('emailTemplate');
                if (template) {
                    document.getElementById('emailTemplate').value = template;
                }
            }

            showNotification(message) {
                // Simple notification - you could make this fancier
                const notification = document.createElement('div');
                notification.style.cssText = `
                    position: fixed;
                    top: 20px;
                    right: 20px;
                    background: #28a745;
                    color: white;
                    padding: 15px 20px;
                    border-radius: 6px;
                    z-index: 1000;
                    animation: slideIn 0.3s ease;
                `;
                notification.textContent = message;
                
                document.body.appendChild(notification);
                
                setTimeout(() => {
                    notification.remove();
                }, 3000);
            }
        }

        // Initialize the app
        const app = new ProspectManager();
    </script>

    <style>
        @keyframes slideIn {
            from { transform: translateX(100%); }
            to { transform: translateX(0); }
        }
    </style>
</body>
</html>

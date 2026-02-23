<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>法律服务智能工作台</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        :root {
            --primary-color: #2563eb;
            --primary-hover: #1d4ed8;
            --secondary-color: #64748b;
            --success-color: #10b981;
            --warning-color: #f59e0b;
            --danger-color: #ef4444;
            --background: #f8fafc;
            --surface: #ffffff;
            --border: #e2e8f0;
            --text-primary: #1e293b;
            --text-secondary: #64748b;
            --shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            --shadow-lg: 0 10px 25px rgba(0, 0, 0, 0.1);
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
            background: var(--background);
            color: var(--text-primary);
            line-height: 1.6;
            height: 100vh;
            overflow: hidden;
        }

        .header {
            height: 60px;
            background: var(--surface);
            border-bottom: 1px solid var(--border);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 24px;
            box-shadow: var(--shadow);
            z-index: 100;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .logo-icon {
            font-size: 28px;
        }

        .logo-text {
            font-size: 18px;
            font-weight: 600;
            color: var(--text-primary);
        }

        .header-actions {
            display: flex;
            gap: 12px;
        }

        .main-container {
            display: flex;
            height: calc(100vh - 60px);
        }

        .step-panel {
            width: 280px;
            background: var(--surface);
            border-right: 1px solid var(--border);
            display: flex;
            flex-direction: column;
            overflow-y: auto;
        }

        .panel-header {
            padding: 20px;
            border-bottom: 1px solid var(--border);
        }

        .panel-header h3 {
            font-size: 16px;
            font-weight: 600;
            color: var(--text-primary);
        }

        .steps-container {
            padding: 16px;
        }

        .step {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 16px;
            border-radius: 8px;
            margin-bottom: 8px;
            transition: all 0.3s;
            cursor: pointer;
        }

        .step[data-status="active"] {
            background: #eff6ff;
            border-left: 3px solid var(--primary-color);
        }

        .step[data-status="completed"] {
            background: #f0fdf4;
            border-left: 3px solid var(--success-color);
        }

        .step[data-status="pending"] {
            background: var(--surface);
            border-left: 3px solid var(--border);
        }

        .step-icon {
            font-size: 24px;
        }

        .step-content {
            flex: 1;
        }

        .step-title {
            font-size: 14px;
            font-weight: 600;
            color: var(--text-primary);
            margin-bottom: 4px;
        }

        .step-desc {
            font-size: 12px;
            color: var(--text-secondary);
        }

        .status-badge {
            font-size: 11px;
            padding: 4px 8px;
            border-radius: 4px;
            font-weight: 500;
        }

        .status-badge.active {
            background: var(--primary-color);
            color: white;
        }

        .status-badge.completed {
            background: var(--success-color);
            color: white;
        }

        .status-badge.pending {
            background: var(--border);
            color: var(--text-secondary);
        }

        .workspace {
            flex: 1;
            display: flex;
            flex-direction: column;
            background: var(--background);
            overflow: hidden;
        }

        .workspace-tabs {
            display: flex;
            gap: 8px;
            padding: 16px 24px 0;
            background: var(--surface);
            border-bottom: 1px solid var(--border);
        }

        .tab {
            padding: 12px 20px;
            background: transparent;
            border: none;
            border-bottom: 2px solid transparent;
            font-size: 14px;
            font-weight: 500;
            color: var(--text-secondary);
            cursor: pointer;
            transition: all 0.3s;
        }

        .tab:hover {
            color: var(--primary-color);
        }

        .tab.active {
            color: var(--primary-color);
            border-bottom-color: var(--primary-color);
        }

        .panel {
            display: none;
            flex: 1;
            overflow-y: auto;
            padding: 24px;
        }

        .panel.active {
            display: block;
        }

        .panel-content {
            max-width: 800px;
            margin: 0 auto;
        }

        .form-section {
            background: var(--surface);
            border-radius: 12px;
            padding: 24px;
            margin-bottom: 20px;
            box-shadow: var(--shadow);
        }

        .form-section h3 {
            font-size: 16px;
            font-weight: 600;
            color: var(--text-primary);
            margin-bottom: 16px;
        }

        .radio-group {
            display: flex;
            gap: 24px;
        }

        .radio-label {
            display: flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
        }

        .radio-custom {
            width: 20px;
            height: 20px;
            border: 2px solid var(--border);
            border-radius: 50%;
            position: relative;
            transition: all 0.3s;
        }

        .radio-label input:checked + .radio-custom {
            border-color: var(--primary-color);
        }

        .radio-label input:checked + .radio-custom::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 10px;
            height: 10px;
            background: var(--primary-color);
            border-radius: 50%;
        }

        .radio-text {
            font-size: 14px;
            color: var(--text-primary);
        }

        .form-select,
        .form-input,
        .form-textarea {
            width: 100%;
            padding: 12px 16px;
            border: 1px solid var(--border);
            border-radius: 8px;
            font-size: 14px;
            color: var(--text-primary);
            background: var(--surface);
            transition: all 0.3s;
        }

        .form-select:focus,
        .form-input:focus,
        .form-textarea:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
        }

        .form-textarea {
            resize: vertical;
            min-height: 120px;
        }

        .input-group {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .input-group .form-input {
            flex: 1;
        }

        .input-suffix {
            font-size: 14px;
            color: var(--text-secondary);
        }

        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background: var(--primary-color);
            color: white;
        }

        .btn-primary:hover {
            background: var(--primary-hover);
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
        }

        .btn-primary:disabled {
            background: var(--secondary-color);
            cursor: not-allowed;
            transform: none;
        }

        .btn-secondary {
            background: var(--surface);
            color: var(--text-primary);
            border: 1px solid var(--border);
        }

        .btn-secondary:hover {
            background: var(--background);
            border-color: var(--secondary-color);
        }

        .form-actions {
            display: flex;
            gap: 12px;
            justify-content: flex-end;
        }

        .chat-container {
            display: flex;
            flex-direction: column;
            height: 100%;
            background: var(--surface);
            border-radius: 12px;
            box-shadow: var(--shadow);
        }

        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 24px;
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .message {
            display: flex;
            gap: 12px;
            max-width: 80%;
        }

        .message.user {
            align-self: flex-end;
            flex-direction: row-reverse;
        }

        .message-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            flex-shrink: 0;
        }

        .message.assistant .message-avatar {
            background: #eff6ff;
        }

        .message.user .message-avatar {
            background: #f0fdf4;
        }

        .message-content {
            padding: 12px 16px;
            border-radius: 12px;
            font-size: 14px;
            line-height: 1.6;
        }

        .message.assistant .message-content {
            background: #eff6ff;
            color: var(--text-primary);
        }

        .message.user .message-content {
            background: var(--primary-color);
            color: white;
        }

        .chat-input-area {
            padding: 16px;
            border-top: 1px solid var(--border);
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .chat-input {
            width: 100%;
            padding: 12px;
            border: 1px solid var(--border);
            border-radius: 8px;
            font-size: 14px;
            resize: none;
            font-family: inherit;
        }

        .chat-input:focus {
            outline: none;
            border-color: var(--primary-color);
        }

        .chat-actions {
            display: flex;
            gap: 8px;
            justify-content: flex-end;
        }

        .result-container {
            max-width: 1000px;
            margin: 0 auto;
        }

        .result-summary {
            background: var(--surface);
            border-radius: 12px;
            padding: 24px;
            margin-bottom: 20px;
            box-shadow: var(--shadow);
        }

        .result-summary h3 {
            font-size: 16px;
            font-weight: 600;
            color: var(--text-primary);
            margin-bottom: 16px;
        }

        .summary-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 16px;
        }

        .summary-card {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 16px;
            background: var(--background);
            border-radius: 8px;
        }

        .card-icon {
            font-size: 32px;
        }

        .card-content {
            flex: 1;
        }

        .card-label {
            font-size: 12px;
            color: var(--text-secondary);
            margin-bottom: 4px;
        }

        .card-value {
            font-size: 16px;
            font-weight: 600;
            color: var(--text-primary);
        }

        .result-tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
        }

        .result-tab {
            padding: 10px 20px;
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: 8px;
            font-size: 14px;
            font-weight: 500;
            color: var(--text-secondary);
            cursor: pointer;
            transition: all 0.3s;
        }

        .result-tab:hover {
            border-color: var(--primary-color);
            color: var(--primary-color);
        }

        .result-tab.active {
            background: var(--primary-color);
            border-color: var(--primary-color);
            color: white;
        }

        .result-content {
            background: var(--surface);
            border-radius: 12px;
            padding: 24px;
            box-shadow: var(--shadow);
        }

        .result-detail {
            display: none;
        }

        .result-detail.active {
            display: block;
        }

        .result-detail h4 {
            font-size: 14px;
            font-weight: 600;
            color: var(--text-primary);
            margin-bottom: 12px;
        }

        .detail-content {
            font-size: 14px;
            line-height: 1.8;
            color: var(--text-primary);
        }

        .tool-panel {
            width: 240px;
            background: var(--surface);
            border-left: 1px solid var(--border);
            display: flex;
            flex-direction: column;
            overflow-y: auto;
        }

        .tools-container {
            padding: 16px;
        }

        .tool-group {
            margin-bottom: 24px;
        }

        .group-title {
            font-size: 12px;
            font-weight: 600;
            color: var(--text-secondary);
            text-transform: uppercase;
            margin-bottom: 12px;
            padding-left: 8px;
        }

        .tool-btn {
            width: 100%;
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px;
            background: transparent;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            margin-bottom: 4px;
        }

        .tool-btn:hover {
            background: var(--background);
        }

        .tool-icon {
            font-size: 20px;
        }

        .tool-text {
            font-size: 13px;
            color: var(--text-primary);
            text-align: left;
        }

        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: #fff;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .document-section {
            background: var(--surface);
            border-radius: 12px;
            padding: 24px;
            margin-top: 20px;
            box-shadow: var(--shadow);
        }

        .document-section h3 {
            font-size: 16px;
            font-weight: 600;
            color: var(--text-primary);
            margin-bottom: 16px;
        }

        .document-actions {
            display: flex;
            gap: 12px;
            margin-top: 16px;
        }

        .document-preview {
            background: var(--background);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 20px;
            margin-top: 16px;
            max-height: 400px;
            overflow-y: auto;
            font-family: 'Courier New', monospace;
            white-space: pre-wrap;
            font-size: 13px;
            line-height: 1.6;
        }

        .demo-content {
            padding: 12px;
            background: var(--background);
            border-radius: 8px;
            margin: 12px 0;
        }

        .demo-content h5 {
            color: var(--primary-color);
            margin-bottom: 8px;
        }

        .demo-content ul {
            padding-left: 20px;
        }

        .demo-content li {
            margin: 4px 0;
        }

        .demo-content table {
            width: 100%;
            border-collapse: collapse;
        }

        .demo-content td {
            padding: 8px;
            border: 1px solid #ddd;
        }

        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }

        .modal-overlay.active {
            display: flex;
        }

        .modal {
            background: var(--surface);
            border-radius: 12px;
            box-shadow: var(--shadow-lg);
            max-width: 600px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
        }

        .modal-header {
            padding: 20px;
            border-bottom: 1px solid var(--border);
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .modal-title {
            font-size: 18px;
            font-weight: 600;
            color: var(--text-primary);
        }

        .modal-close {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: var(--text-secondary);
        }

        .modal-body {
            padding: 24px;
        }

        .modal-footer {
            padding: 16px 24px;
            border-top: 1px solid var(--border);
            display: flex;
            gap: 12px;
            justify-content: flex-end;
        }

        .toast-container {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 1001;
        }

        .toast {
            padding: 16px 20px;
            border-radius: 8px;
            margin-bottom: 12px;
            box-shadow: var(--shadow-lg);
            animation: slideIn 0.3s ease-out;
        }

        .toast.success {
            background: var(--success-color);
            color: white;
        }

        .toast.error {
            background: var(--danger-color);
            color: white;
        }

        .toast.warning {
            background: var(--warning-color);
            color: white;
        }

        .toast.info {
            background: var(--primary-color);
            color: white;
        }

        @keyframes slideIn {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        @media (max-width: 1400px) {
            .step-panel {
                width: 240px;
            }
            
            .tool-panel {
                width: 200px;
            }
        }

        @media (max-width: 1200px) {
            .step-panel,
            .tool-panel {
                display: none;
            }
        }
    </style>
</head>
<body>
    <header class="header">
        <div class="logo">
            <span class="logo-icon">⚖️</span>
            <span class="logo-text">法律服务智能工作台</span>
        </div>
        <div class="header-actions">
            <button class="btn btn-secondary" onclick="resetWorkspace()">新建案件</button>
            <button class="btn btn-secondary" onclick="showApiConfig()">API配置</button>
        </div>
    </header>

    <div class="main-container">
        <aside class="step-panel">
            <div class="panel-header">
                <h3>工作流程</h3>
            </div>
            <div class="steps-container">
                <div class="step" data-step="1" data-status="active">
                    <div class="step-icon">👤</div>
                    <div class="step-content">
                        <div class="step-title">1. 角色识别</div>
                        <div class="step-desc">选择原告或被告</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge active">进行中</span>
                    </div>
                </div>

                <div class="step" data-step="2" data-status="pending">
                    <div class="step-icon">📋</div>
                    <div class="step-content">
                        <div class="step-title">2. 案由识别</div>
                        <div class="step-desc">识别案件类型</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge pending">待开始</span>
                    </div>
                </div>

                <div class="step" data-step="3" data-status="pending">
                    <div class="step-icon">📝</div>
                    <div class="step-content">
                        <div class="step-title">3. 案件信息录入</div>
                        <div class="step-desc">录入案件详细信息</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge pending">待开始</span>
                    </div>
                </div>

                <div class="step" data-step="4" data-status="pending">
                    <div class="step-icon">🔍</div>
                    <div class="step-content">
                        <div class="step-title">4. 智能分析</div>
                        <div class="step-desc">AI分析案件</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge pending">待开始</span>
                    </div>
                </div>

                <div class="step" data-step="5" data-status="pending">
                    <div class="step-icon">📚</div>
                    <div class="step-content">
                        <div class="step-title">5. 法律查询</div>
                        <div class="step-desc">查询相关法律条文</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge pending">待开始</span>
                    </div>
                </div>

                <div class="step" data-step="6" data-status="pending">
                    <div class="step-icon">⚖️</div>
                    <div class="step-content">
                        <div class="step-title">6. 案例分析</div>
                        <div class="step-desc">分析相似案例</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge pending">待开始</span>
                    </div>
                </div>

                <div class="step" data-step="7" data-status="pending">
                    <div class="step-icon">📄</div>
                    <div class="step-content">
                        <div class="step-title">7. 文书生成</div>
                        <div class="step-desc">生成法律文书</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge pending">待开始</span>
                    </div>
                </div>

                <div class="step" data-step="8" data-status="pending">
                    <div class="step-icon">✅</div>
                    <div class="step-content">
                        <div class="step-title">8. 完成</div>
                        <div class="step-desc">案件处理完成</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge pending">待开始</span>
                    </div>
                </div>
            </div>
        </aside>

        <main class="workspace">
            <div class="workspace-tabs">
                <button class="tab active" data-tab="input">信息录入</button>
                <button class="tab" data-tab="chat">智能对话</button>
                <button class="tab" data-tab="result">处理结果</button>
            </div>

            <div class="panel active" id="panel-input">
                <div class="panel-content">
                    <div class="form-section">
                        <h3>👤 角色选择</h3>
                        <div class="radio-group">
                            <label class="radio-label">
                                <input type="radio" name="role" value="plaintiff" checked>
                                <span class="radio-custom"></span>
                                <span class="radio-text">原告</span>
                            </label>
                            <label class="radio-label">
                                <input type="radio" name="role" value="defendant">
                                <span class="radio-custom"></span>
                                <span class="radio-text">被告</span>
                            </label>
                        </div>
                    </div>

                    <div class="form-section">
                        <h3>📋 案由选择</h3>
                        <select class="form-select" id="caseType">
                            <option value="">请选择案由</option>
                            <option value="离婚纠纷">离婚纠纷</option>
                            <option value="抚养费纠纷">抚养费纠纷</option>
                            <option value="买卖合同纠纷">买卖合同纠纷</option>
                            <option value="借款合同纠纷">借款合同纠纷</option>
                            <option value="房屋租赁合同纠纷">房屋租赁合同纠纷</option>
                            <option value="物业服务合同纠纷">物业服务合同纠纷</option>
                            <option value="机动车交通事故责任纠纷">机动车交通事故责任纠纷</option>
                            <option value="名誉权纠纷">名誉权纠纷</option>
                            <option value="肖像权纠纷">肖像权纠纷</option>
                            <option value="劳动合同纠纷">劳动合同纠纷</option>
                            <option value="股权转让纠纷">股权转让纠纷</option>
                            <option value="著作权侵权纠纷">著作权侵权纠纷</option>
                        </select>
                    </div>

                    <div class="form-section">
                        <h3>📝 案件详情</h3>
                        <textarea class="form-textarea" id="caseDescription" rows="8" placeholder="请详细描述案件情况，包括事件经过、争议焦点、诉讼请求等..."></textarea>
                    </div>

                    <div class="form-section">
                        <h3>💰 争议金额</h3>
                        <div class="input-group">
                            <input type="number" class="form-input" id="claimAmount" placeholder="请输入争议金额">
                            <span class="input-suffix">元</span>
                        </div>
                    </div>

                    <div class="form-actions">
                        <button class="btn btn-secondary" onclick="clearForm()">清空</button>
                        <button class="btn btn-primary" id="submitBtn" onclick="submitCase()">开始分析</button>
                    </div>
                </div>
            </div>

            <div class="panel" id="panel-chat">
                <div class="chat-container">
                    <div class="chat-messages" id="chatMessages">
                        <div class="message assistant">
                            <div class="message-avatar">🤖</div>
                            <div class="message-content">
                                <p>您好！我是您的法律服务智能助手。请告诉我您的案件情况，我会为您提供专业的法律服务。</p>
                            </div>
                        </div>
                    </div>
                    <div class="chat-input-area">
                        <textarea class="chat-input" id="chatInput" rows="3" placeholder="请输入您的问题或描述..."></textarea>
                        <div class="chat-actions">
                            <button class="btn btn-primary" id="sendBtn" onclick="sendMessage()">发送</button>
                        </div>
                    </div>
                </div>
            </div>

            <div class="panel" id="panel-result">
                <div class="result-container">
                    <div class="result-summary">
                        <h3>📊 案件分析摘要</h3>
                        <div class="summary-cards">
                            <div class="summary-card">
                                <div class="card-icon">⚖️</div>
                                <div class="card-content">
                                    <div class="card-label">案件类型</div>
                                    <div class="card-value" id="resultCaseType">-</div>
                                </div>
                            </div>
                            <div class="summary-card">
                                <div class="card-icon">👤</div>
                                <div class="card-content">
                                    <div class="card-label">当事人角色</div>
                                    <div class="card-value" id="resultRole">-</div>
                                </div>
                            </div>
                            <div class="summary-card">
                                <div class="card-icon">💰</div>
                                <div class="card-content">
                                    <div class="card-label">争议金额</div>
                                    <div class="card-value" id="resultAmount">-</div>
                                </div>
                            </div>
                            <div class="summary-card">
                                <div class="card-icon">📈</div>
                                <div class="card-content">
                                    <div class="card-label">胜诉率评估</div>
                                    <div class="card-value" id="resultWinRate">-</div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="result-tabs">
                        <button class="result-tab active" data-result-tab="legal">法律依据</button>
                        <button class="result-tab" data-result-tab="case">相似案例</button>
                        <button class="result-tab" data-result-tab="risk">风险评估</button>
                        <button class="result-tab" data-result-tab="cost">费用计算</button>
                    </div>

                    <div class="result-content">
                        <div class="result-detail active" id="result-legal">
                            <h4>📚 相关法律条文</h4>
                            <div id="legalContent" class="detail-content">
                                <p>请先进行案件分析</p>
                            </div>
                        </div>

                        <div class="result-detail" id="result-case">
                            <h4>📋 相似案例</h4>
                            <div id="caseContent" class="detail-content">
                                <p>请先进行案件分析</p>
                            </div>
                        </div>

                        <div class="result-detail" id="result-risk">
                            <h4>⚠️ 风险评估</h4>
                            <div id="riskContent" class="detail-content">
                                <p>请先进行案件分析</p>
                            </div>
                        </div>

                        <div class="result-detail" id="result-cost">
                            <h4>💰 费用计算</h4>
                            <div id="costContent" class="detail-content">
                                <p>请先进行案件分析</p>
                            </div>
                        </div>
                    </div>

                    <div class="document-section">
                        <h3>📄 文书生成</h3>
                        <div class="document-actions">
                            <button class="btn btn-primary" onclick="generateDocument('起诉状')">生成起诉状</button>
                            <button class="btn btn-primary" onclick="generateDocument('答辩状')">生成答辩状</button>
                            <button class="btn btn-primary" onclick="generateDocument('代理词')">生成代理词</button>
                        </div>
                        <div id="documentPreview" class="document-preview" style="display: none;"></div>
                    </div>
                </div>
            </div>
        </main>

        <aside class="tool-panel">
            <div class="panel-header">
                <h3>快捷工具</h3>
            </div>
            <div class="tools-container">
                <div class="tool-group">
                    <div class="group-title">证据处理</div>
                    <button class="tool-btn" onclick="callTool('parse_evidence')">
                        <span class="tool-icon">🔍</span>
                        <span class="tool-text">解析证据</span>
                    </button>
                    <button class="tool-btn" onclick="callTool('ocr_recognize')">
                        <span class="tool-icon">📷</span>
                        <span class="tool-text">图片OCR识别</span>
                    </button>
                </div>

                <div class="tool-group">
                    <div class="group-title">法律查询</div>
                    <button class="tool-btn" onclick="callTool('search_legal')">
                        <span class="tool-icon">📚</span>
                        <span class="tool-text">查询法条</span>
                    </button>
                    <button class="tool-btn" onclick="callTool('search_case')">
                        <span class="tool-icon">📋</span>
                        <span class="tool-text">搜索案例</span>
                    </button>
                </div>

                <div class="tool-group">
                    <div class="group-title">智能分析</div>
                    <button class="tool-btn" onclick="callTool('similarity')">
                        <span class="tool-icon">⚖️</span>
                        <span class="tool-text">相似度分析</span>
                    </button>
                    <button class="tool-btn" onclick="callTool('prediction')">
                        <span class="tool-icon">🔮</span>
                        <span class="tool-text">判决预测</span>
                    </button>
                    <button class="tool-btn" onclick="callTool('risk')">
                        <span class="tool-icon">⚠️</span>
                        <span class="tool-text">风险评估</span>
                    </button>
                </div>
            </div>
        </aside>
    </div>

    <div class="modal-overlay" id="apiConfigModal">
        <div class="modal">
            <div class="modal-header">
                <h3 class="modal-title">API 配置</h3>
                <button class="modal-close" onclick="closeApiConfig()">×</button>
            </div>
            <div class="modal-body">
                <div class="form-section">
                    <h3>后端API地址</h3>
                    <input type="text" class="form-input" id="apiBaseUrl" placeholder="http://localhost:8000" value="http://localhost:8000">
                </div>
                <div class="form-section">
                    <h3>API Key（可选）</h3>
                    <input type="password" class="form-input" id="apiKey" placeholder="输入API Key">
                </div>
                <p style="color: var(--text-secondary); font-size: 12px;">
                    注意：如果使用本地后端，请确保后端服务已启动（运行 bash scripts/start_ui.sh）
                </p>
            </div>
            <div class="modal-footer">
                <button class="btn btn-secondary" onclick="closeApiConfig()">取消</button>
                <button class="btn btn-primary" onclick="saveApiConfig()">保存配置</button>
            </div>
        </div>
    </div>

    <div class="modal-overlay" id="modalOverlay">
        <div class="modal">
            <div class="modal-header">
                <h3 class="modal-title" id="modalTitle">标题</h3>
                <button class="modal-close" onclick="closeModal()">×</button>
            </div>
            <div class="modal-body" id="modalBody">
                内容
            </div>
            <div class="modal-footer">
                <button class="btn btn-primary" onclick="closeModal()">确定</button>
            </div>
        </div>
    </div>

    <div class="toast-container" id="toastContainer"></div>

    <script>
        // API 配置
        let apiBaseUrl = localStorage.getItem('apiBaseUrl') || 'http://localhost:8000';
        let apiKey = localStorage.getItem('apiKey') || '';

        // 状态管理
        const state = {
            currentStep: 1,
            currentTab: 'input',
            currentResultTab: 'legal',
            chatHistory: [],
            caseData: {
                role: 'plaintiff',
                caseType: '',
                caseDescription: '',
                claimAmount: 0
            },
            analysisResult: null
        };

        // 初始化
        document.addEventListener('DOMContentLoaded', function() {
            initializeTabs();
            initializeResultTabs();
            initializeChat();
            loadApiConfig();
        });

        // 加载 API 配置
        function loadApiConfig() {
            document.getElementById('apiBaseUrl').value = apiBaseUrl;
            document.getElementById('apiKey').value = apiKey;
        }

        // 显示 API 配置
        function showApiConfig() {
            document.getElementById('apiConfigModal').classList.add('active');
        }

        // 关闭 API 配置
        function closeApiConfig() {
            document.getElementById('apiConfigModal').classList.remove('active');
        }

        // 保存 API 配置
        function saveApiConfig() {
            apiBaseUrl = document.getElementById('apiBaseUrl').value.trim();
            apiKey = document.getElementById('apiKey').value.trim();
            
            localStorage.setItem('apiBaseUrl', apiBaseUrl);
            localStorage.setItem('apiKey', apiKey);
            
            closeApiConfig();
            showToast('API配置已保存', 'success');
        }

        // 初始化标签页
        function initializeTabs() {
            const tabs = document.querySelectorAll('.tab');
            tabs.forEach(tab => {
                tab.addEventListener('click', function() {
                    const tabName = this.dataset.tab;
                    switchTab(tabName);
                });
            });
        }

        function switchTab(tabName) {
            state.currentTab = tabName;
            
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.toggle('active', tab.dataset.tab === tabName);
            });
            
            document.querySelectorAll('.panel').forEach(panel => {
                panel.classList.toggle('active', panel.id === `panel-${tabName}`);
            });
        }

        // 初始化结果标签页
        function initializeResultTabs() {
            const tabs = document.querySelectorAll('.result-tab');
            tabs.forEach(tab => {
                tab.addEventListener('click', function() {
                    const tabName = this.dataset.resultTab;
                    switchResultTab(tabName);
                });
            });
        }

        function switchResultTab(tabName) {
            state.currentResultTab = tabName;
            
            document.querySelectorAll('.result-tab').forEach(tab => {
                tab.classList.toggle('active', tab.dataset.resultTab === tabName);
            });
            
            document.querySelectorAll('.result-detail').forEach(detail => {
                detail.classList.toggle('active', detail.id === `result-${tabName}`);
            });
        }

        // 初始化聊天
        function initializeChat() {
            const chatInput = document.getElementById('chatInput');
            
            chatInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    sendMessage();
                }
            });
        }

        // 发送消息
        async function sendMessage() {
            const chatInput = document.getElementById('chatInput');
            const message = chatInput.value.trim();
            
            if (!message) return;
            
            // 添加用户消息
            addChatMessage('user', message);
            chatInput.value = '';
            
            // 禁用发送按钮
            const sendBtn = document.getElementById('sendBtn');
            sendBtn.disabled = true;
            sendBtn.innerHTML = '<div class="loading"></div>';
            
            try {
                // 调用后端 API
                const response = await fetch(`${apiBaseUrl}/api/chat`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': apiKey ? `Bearer ${apiKey}` : ''
                    },
                    body: JSON.stringify({
                        prompt: message,
                        case_data: state.caseData,
                        history: state.chatHistory
                    })
                });
                
                if (!response.ok) {
                    throw new Error('API请求失败');
                }
                
                const data = await response.json();
                
                // 添加AI回复
                addChatMessage('assistant', data.response);
                
                // 保存到历史
                state.chatHistory.push({role: 'user', content: message});
                state.chatHistory.push({role: 'assistant', content: data.response});
                
            } catch (error) {
                console.error('Error:', error);
                addChatMessage('assistant', '抱歉，连接后端服务失败。请检查后端服务是否启动，或者配置正确的API地址。');
            } finally {
                sendBtn.disabled = false;
                sendBtn.innerHTML = '发送';
            }
        }

        // 添加聊天消息
        function addChatMessage(role, content) {
            const chatMessages = document.getElementById('chatMessages');
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${role}`;
            messageDiv.innerHTML = `
                <div class="message-avatar">${role === 'user' ? '👤' : '🤖'}</div>
                <div class="message-content">${escapeHtml(content)}</div>
            `;
            chatMessages.appendChild(messageDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        // 清空表单
        function clearForm() {
            document.getElementById('caseType').value = '';
            document.getElementById('caseDescription').value = '';
            document.getElementById('claimAmount').value = '';
            state.caseData.caseType = '';
            state.caseData.caseDescription = '';
            state.caseData.claimAmount = 0;
        }

        // 提交案件分析
        async function submitCase() {
            const role = document.querySelector('input[name="role"]:checked').value;
            const caseType = document.getElementById('caseType').value;
            const caseDescription = document.getElementById('caseDescription').value;
            const claimAmount = document.getElementById('claimAmount').value;
            
            if (!caseType) {
                showToast('请选择案由', 'warning');
                return;
            }
            
            if (!caseDescription.trim()) {
                showToast('请填写案件详情', 'warning');
                return;
            }
            
            // 更新状态
            state.caseData.role = role;
            state.caseData.caseType = caseType;
            state.caseData.caseDescription = caseDescription;
            state.caseData.claimAmount = parseFloat(claimAmount) || 0;
            
            // 更新步骤状态
            updateStepStatus(2, 'completed');
            updateStepStatus(3, 'completed');
            
            // 禁用提交按钮
            const submitBtn = document.getElementById('submitBtn');
            submitBtn.disabled = true;
            submitBtn.innerHTML = '<div class="loading"></div>';
            
            showToast('正在分析案件，请稍候...', 'info');
            
            try {
                // 调用后端分析 API
                const response = await fetch(`${apiBaseUrl}/api/analyze`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': apiKey ? `Bearer ${apiKey}` : ''
                    },
                    body: JSON.stringify({
                        role: role,
                        case_type: caseType,
                        case_description: caseDescription,
                        claim_amount: parseFloat(claimAmount) || 0
                    })
                });
                
                if (!response.ok) {
                    throw new Error('分析失败');
                }
                
                const result = await response.json();
                state.analysisResult = result;
                
                // 更新结果展示
                updateResultDisplay(result);
                
                showToast('案件分析完成', 'success');
                switchTab('result');
                
                // 更新步骤状态
                for (let i = 4; i <= 6; i++) {
                    updateStepStatus(i, 'completed');
                }
                
            } catch (error) {
                console.error('Error:', error);
                showToast('分析失败，请检查后端服务', 'error');
                
                // 使用模拟数据作为后备
                useDemoData();
                
            } finally {
                submitBtn.disabled = false;
                submitBtn.innerHTML = '开始分析';
            }
        }

        // 更新结果展示
        function updateResultDisplay(result) {
            document.getElementById('resultCaseType').textContent = state.caseData.caseType;
            document.getElementById('resultRole').textContent = state.caseData.role === 'plaintiff' ? '原告' : '被告';
            document.getElementById('resultAmount').textContent = state.caseData.claimAmount ? 
                `¥${state.caseData.claimAmount.toLocaleString()}` : '-';
            document.getElementById('resultWinRate').textContent = result.win_rate || '85% - 90%';
            
            // 更新详细内容
            if (result.legal_basis) {
                document.getElementById('legalContent').innerHTML = formatContent(result.legal_basis);
            }
            if (result.similar_cases) {
                document.getElementById('caseContent').innerHTML = formatContent(result.similar_cases);
            }
            if (result.risk_assessment) {
                document.getElementById('riskContent').innerHTML = formatContent(result.risk_assessment);
            }
            if (result.cost_calculation) {
                document.getElementById('costContent').innerHTML = formatContent(result.cost_calculation);
            }
        }

        // 使用模拟数据
        function useDemoData() {
            const demoResult = {
                win_rate: '85% - 90%',
                legal_basis: `
                    <div class="demo-content">
                        <h5>一、《中华人民共和国民法典》相关条文</h5>
                        <ul>
                            <li><strong>第六百六十七条</strong> 借款合同是借款人向贷款人借款，到期返还借款并支付利息的合同。</li>
                            <li><strong>第六百七十九条</strong> 自然人之间的借款合同，自贷款人提供借款时成立。</li>
                            <li><strong>第六百八十条</strong> 禁止高利放贷，借款的利率不得违反国家有关规定。</li>
                        </ul>
                        <br>
                        <h5>二、《中华人民共和国民事诉讼法》相关条文</h5>
                        <ul>
                            <li><strong>第一百一十九条</strong> 起诉必须符合下列条件：（一）原告是与本案有直接利害关系的公民、法人和其他组织；（二）有明确的被告；（三）有具体的诉讼请求和事实、理由；（四）属于人民法院受理民事诉讼的范围和受诉人民法院管辖。</li>
                        </ul>
                    </div>
                `,
                similar_cases: `
                    <div class="demo-content">
                        <h5>相似案例1：张三诉李四借款合同纠纷案</h5>
                        <p><strong>案情概述：</strong>原告张三与被告李四签订借款合同，借款50万元，约定月利率2%，借款期限1年。被告逾期未还。</p>
                        <p><strong>判决结果：</strong>法院判决被告偿还借款本金50万元及利息，利息按年利率24%计算。</p>
                        <p><strong>胜诉率：</strong>95%</p>
                        <hr>
                        <h5>相似案例2：王五诉赵六民间借贷纠纷案</h5>
                        <p><strong>案情概述：</strong>原告王五出借30万元给被告赵六，有借条和转账记录为证，被告未按期还款。</p>
                        <p><strong>判决结果：</strong>法院支持原告全部诉讼请求，被告需偿还本金及利息。</p>
                        <p><strong>胜诉率：</strong>90%</p>
                    </div>
                `,
                risk_assessment: `
                    <div class="demo-content">
                        <h5>一、法律风险</h5>
                        <ul>
                            <li>借款合同有效性：<span style="color: green;">低风险</span> - 有完整借条和转账记录</li>
                            <li>诉讼时效：<span style="color: green;">低风险</span> - 在三年诉讼时效内</li>
                        </ul>
                        <br>
                        <h5>二、事实认定风险</h5>
                        <ul>
                            <li>借款事实：<span style="color: green;">低风险</span> - 证据充分</li>
                            <li>利息约定：<span style="color: orange;">中等风险</span> - 需确认利率是否合法</li>
                        </ul>
                        <br>
                        <h5>三、执行风险</h5>
                        <ul>
                            <li>被告偿债能力：<span style="color: orange;">中等风险</span> - 需调查被告财产状况</li>
                        </ul>
                        <br>
                        <h5>综合风险评估：<span style="color: green;">低风险</span></h5>
                        <p><strong>建议：</strong>建议提起诉讼，胜诉可能性较高。</p>
                    </div>
                `,
                cost_calculation: `
                    <div class="demo-content">
                        <h5>一、诉讼费用</h5>
                        <table style="width: 100%; border-collapse: collapse;">
                            <tr style="background: #f0f0f0;">
                                <td style="padding: 8px; border: 1px solid #ddd;"><strong>费用项目</strong></td>
                                <td style="padding: 8px; border: 1px solid #ddd;"><strong>金额（元）</strong></td>
                            </tr>
                            <tr>
                                <td style="padding: 8px; border: 1px solid #ddd;">案件受理费</td>
                                <td style="padding: 8px; border: 1px solid #ddd;">10,500.00</td>
                            </tr>
                            <tr>
                                <td style="padding: 8px; border: 1px solid #ddd;">保全费</td>
                                <td style="padding: 8px; border: 1px solid #ddd;">5,000.00</td>
                            </tr>
                            <tr style="font-weight: bold; background: #f9f9f9;">
                                <td style="padding: 8px; border: 1px solid #ddd;">小计</td>
                                <td style="padding: 8px; border: 1px solid #ddd;">15,500.00</td>
                            </tr>
                        </table>
                        <br>
                        <h5>二、律师费用</h5>
                        <p>按争议金额的4%-8%计算：<strong>20,000 - 40,000元</strong></p>
                        <br>
                        <h5>三、费用总计</h5>
                        <p style="font-size: 18px; color: var(--primary-color);"><strong>约 35,500 - 55,500 元</strong></p>
                    </div>
                `
            };
            
            updateResultDisplay(demoResult);
        }

        // 格式化内容
        function formatContent(content) {
            if (typeof content === 'string') {
                return content.replace(/\n/g, '<br>');
            }
            return content;
        }

        // 更新步骤状态
        function updateStepStatus(stepNumber, status) {
            const step = document.querySelector(`.step[data-step="${stepNumber}"]`);
            if (step) {
                step.dataset.status = status;
                const badge = step.querySelector('.status-badge');
                if (badge) {
                    badge.className = `status-badge ${status}`;
                    badge.textContent = status === 'active' ? '进行中' : 
                                      status === 'completed' ? '已完成' : '待开始';
                }
            }
        }

        // 生成文书
        async function generateDocument(docType) {
            if (!state.analysisResult && !state.caseData.caseType) {
                showToast('请先进行案件分析', 'warning');
                return;
            }
            
            showToast(`正在生成${docType}...`, 'info');
            
            try {
                // 调用后端文书生成 API
                const response = await fetch(`${apiBaseUrl}/api/generate-document`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': apiKey ? `Bearer ${apiKey}` : ''
                    },
                    body: JSON.stringify({
                        type: docType,
                        case_data: state.caseData
                    })
                });
                
                if (!response.ok) {
                    throw new Error('生成失败');
                }
                
                const result = await response.json();
                
                if (result.success && result.content) {
                    displayDocument(result.content);
                    showToast(`${docType}生成成功`, 'success');
                    updateStepStatus(7, 'completed');
                } else {
                    throw new Error(result.error || '生成失败');
                }
                
            } catch (error) {
                console.error('Error:', error);
                showToast('生成失败，使用演示数据', 'warning');
                generateDemoDocument(docType);
            }
        }

        // 显示文书
        function displayDocument(content) {
            const preview = document.getElementById('documentPreview');
            preview.style.display = 'block';
            preview.textContent = content;
            
            // 添加下载按钮
            const downloadBtn = document.createElement('button');
            downloadBtn.className = 'btn btn-primary';
            downloadBtn.textContent = '下载文档';
            downloadBtn.onclick = () => downloadDocument(content);
            
            preview.appendChild(downloadBtn);
        }

        // 下载文档
        function downloadDocument(content) {
            const blob = new Blob([content], { type: 'text/plain;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = '法律文书.txt';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        // 生成演示文书
        function generateDemoDocument(docType) {
            const demoContent = getDemoDocumentContent(docType);
            displayDocument(demoContent);
            updateStepStatus(7, 'completed');
        }

        // 获取演示文书内容
        function getDemoDocumentContent(docType) {
            const role = state.caseData.role === 'plaintiff' ? '原告' : '被告';
            const caseType = state.caseData.caseType || '借款合同纠纷';
            
            switch(docType) {
                case '起诉状':
                    return `民事起诉状

原告：[原告姓名]，[性别]，[民族]，[出生日期]，住址：[地址]
被告：[被告姓名]，[性别]，[民族]，[出生日期]，住址：[地址]

诉讼请求：
1. 判令被告偿还原告借款本金${state.caseData.claimAmount || 500000}元；
2. 判令被告支付利息（按年利率24%计算，自借款之日起至实际还款之日止）；
3. 本案诉讼费用由被告承担。

事实与理由：
${state.caseData.caseDescription || '被告于2023年1月向原告借款，约定借款期限1年，利息按月利率2%计算。借款到期后，被告未按约定还款。原告多次催讨未果，为维护原告合法权益，特向贵院提起诉讼。'}

综上所述，为维护原告的合法权益，特向贵院提起诉讼，恳请贵院查明事实，依法支持原告的全部诉讼请求。

此致
[法院名称]

具状人：[原告姓名]
[日期]

附：
1. 借条复印件
2. 银行转账记录`;

                case '答辩状':
                    return `民事答辩状

答辩人：[答辩人姓名]，[性别]，[民族]，[出生日期]，住址：[地址]

因[原告姓名]诉[答辩人姓名][案件类型]一案，提出答辩如下：

答辩请求：
1. 请求法院驳回原告的全部诉讼请求；
2. 本案诉讼费用由原告承担。

事实与理由：
${state.caseData.caseDescription || '关于原告诉称的借款事实，答辩人认为：第一，双方之间不存在真实的借贷关系；第二，即使存在借贷关系，原告主张的利息标准也超过了法律保护的范围；第三，原告未能提供完整的证据链证明其主张。'}

综上所述，原告的诉讼请求缺乏事实和法律依据，恳请贵院依法驳回原告的全部诉讼请求。

此致
[法院名称]

答辩人：[答辩人姓名]
[日期]`;

                case '代理词':
                    return `代理词

尊敬的审判长、审判员：

[律师事务所名称]接受[委托人姓名]的委托，指派我担任其与[对方当事人][案件类型]一案的诉讼代理人。现根据本案事实和相关法律规定，发表如下代理意见：

一、关于案件基本事实
${state.caseData.caseDescription || '本案的基本事实是：双方当事人于2023年1月达成借款合意，原告已实际履行出借义务，被告未按约定偿还借款本息。'}

二、关于法律适用
根据《中华人民共和国民法典》第六百六十七条、第六百七十九条、第六百八十条之规定，借款合同是借款人向贷款人借款，到期返还借款并支付利息的合同。自然人之间的借款合同，自贷款人提供借款时成立。

三、代理意见
1. 原被告之间的借款合同合法有效，应当受到法律保护；
2. 被告未按约定履行还款义务，已构成违约；
3. 原告主张的利息计算标准符合法律规定；
4. 本案诉讼费用应当由被告承担。

综上所述，恳请贵院查明事实，依法支持原告的全部诉讼请求，维护当事人的合法权益。

此致
[法院名称]

代理人：[律师姓名]
[律师事务所名称]
[日期]`;

                default:
                    return '未知的文书类型';
            }
        }

        // 调用工具
        async function callTool(toolName) {
            showToast(`正在调用${toolName}...`, 'info');
            
            try {
                const response = await fetch(`${apiBaseUrl}/api/tool`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': apiKey ? `Bearer ${apiKey}` : ''
                    },
                    body: JSON.stringify({
                        tool: toolName,
                        params: {},
                        case_data: state.caseData
                    })
                });
                
                if (!response.ok) {
                    throw new Error('工具调用失败');
                }
                
                const result = await response.json();
                
                if (result.success && result.result) {
                    showModal(toolName, result.result);
                    showToast(`${toolName}执行成功`, 'success');
                } else {
                    throw new Error(result.error || '执行失败');
                }
                
            } catch (error) {
                console.error('Error:', error);
                showModal(toolName, '工具调用失败，请检查后端服务');
            }
        }

        // 显示弹窗
        function showModal(title, content) {
            document.getElementById('modalTitle').textContent = title;
            document.getElementById('modalBody').innerHTML = content;
            document.getElementById('modalOverlay').classList.add('active');
        }

        // 关闭弹窗
        function closeModal() {
            document.getElementById('modalOverlay').classList.remove('active');
        }

        // 显示提示
        function showToast(message, type = 'info') {
            const container = document.getElementById('toastContainer');
            
            const toast = document.createElement('div');
            toast.className = `toast ${type}`;
            toast.textContent = message;
            
            container.appendChild(toast);
            
            setTimeout(() => {
                toast.style.animation = 'slideIn 0.3s ease-out reverse';
                setTimeout(() => {
                    toast.remove();
                }, 300);
            }, 3000);
        }

        // 转义HTML
        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        // 重置工作区
        function resetWorkspace() {
            if (confirm('确定要新建案件吗？当前数据将被清除。')) {
                clearForm();
                
                for (let i = 1; i <= 8; i++) {
                    updateStepStatus(i, i === 1 ? 'active' : 'pending');
                }
                
                document.getElementById('resultCaseType').textContent = '-';
                document.getElementById('resultRole').textContent = '-';
                document.getElementById('resultAmount').textContent = '-';
                document.getElementById('resultWinRate').textContent = '-';
                document.getElementById('legalContent').innerHTML = '<p>请先进行案件分析</p>';
                document.getElementById('caseContent').innerHTML = '<p>请先进行案件分析</p>';
                document.getElementById('riskContent').innerHTML = '<p>请先进行案件分析</p>';
                document.getElementById('costContent').innerHTML = '<p>请先进行案件分析</p>';
                document.getElementById('documentPreview').style.display = 'none';
                
                switchTab('input');
                state.chatHistory = [];
                document.getElementById('chatMessages').innerHTML = `
                    <div class="message assistant">
                        <div class="message-avatar">🤖</div>
                        <div class="message-content">
                            <p>您好！我是您的法律服务智能助手。请告诉我您的案件情况，我会为您提供专业的法律服务。</p>
                        </div>
                    </div>
                `;
                
                showToast('工作区已重置', 'success');
            }
        }

        // 点击遮罩关闭弹窗
        document.getElementById('modalOverlay').addEventListener('click', function(e) {
            if (e.target === this) {
                closeModal();
            }
        });

        document.getElementById('apiConfigModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeApiConfig();
            }
        });
    </script>
</body>
</html>

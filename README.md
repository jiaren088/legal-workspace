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

        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        ::-webkit-scrollbar-track {
            background: var(--background);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--border);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--secondary-color);
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
            <button class="btn btn-secondary" onclick="showDemo()">演示数据</button>
            <button class="btn btn-secondary" onclick="toggleFullscreen()">全屏模式</button>
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
                        <div class="step-title">4. 证据分析</div>
                        <div class="step-desc">分析证据材料</div>
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
                    <div class="step-icon">📊</div>
                    <div class="step-content">
                        <div class="step-title">7. 风险评估</div>
                        <div class="step-desc">评估案件风险</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge pending">待开始</span>
                    </div>
                </div>

                <div class="step" data-step="8" data-status="pending">
                    <div class="step-icon">💰</div>
                    <div class="step-content">
                        <div class="step-title">8. 费用计算</div>
                        <div class="step-desc">计算诉讼费用</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge pending">待开始</span>
                    </div>
                </div>

                <div class="step" data-step="9" data-status="pending">
                    <div class="step-icon">📄</div>
                    <div class="step-content">
                        <div class="step-title">9. 文书生成</div>
                        <div class="step-desc">生成法律文书</div>
                    </div>
                    <div class="step-status">
                        <span class="status-badge pending">待开始</span>
                    </div>
                </div>

                <div class="step" data-step="10" data-status="pending">
                    <div class="step-icon">✅</div>
                    <div class="step-content">
                        <div class="step-title">10. 完成</div>
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
                        </select>
                    </div>

                    <div class="form-section">
                        <h3>📝 案件详情</h3>
                        <textarea class="form-textarea" id="caseDescription" rows="6" placeholder="请详细描述案件情况，包括事件经过、争议焦点、诉讼请求等..."></textarea>
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
                        <button class="btn btn-primary" onclick="submitCase()">开始分析</button>
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
                                <p><strong>提示：</strong>本版本为静态演示版本，使用模拟数据。完整功能请连接后端服务器使用。</p>
                            </div>
                        </div>
                    </div>
                    <div class="chat-input-area">
                        <textarea class="chat-input" id="chatInput" rows="3" placeholder="请输入您的问题或描述..."></textarea>
                        <div class="chat-actions">
                            <button class="btn btn-primary" onclick="sendMessage()">发送</button>
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
                                <p>暂无数据，请先进行案件分析或点击"演示数据"查看示例</p>
                            </div>
                        </div>

                        <div class="result-detail" id="result-case">
                            <h4>📋 相似案例</h4>
                            <div id="caseContent" class="detail-content">
                                <p>暂无数据，请先进行案件分析或点击"演示数据"查看示例</p>
                            </div>
                        </div>

                        <div class="result-detail" id="result-risk">
                            <h4>⚠️ 风险评估</h4>
                            <div id="riskContent" class="detail-content">
                                <p>暂无数据，请先进行案件分析或点击"演示数据"查看示例</p>
                            </div>
                        </div>

                        <div class="result-detail" id="result-cost">
                            <h4>💰 费用计算</h4>
                            <div id="costContent" class="detail-content">
                                <p>暂无数据，请先进行案件分析或点击"演示数据"查看示例</p>
                            </div>
                        </div>
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
                    <button class="tool-btn" onclick="showToolDemo('解析证据')">
                        <span class="tool-icon">🔍</span>
                        <span class="tool-text">解析证据</span>
                    </button>
                    <button class="tool-btn" onclick="showToolDemo('分析证据清单')">
                        <span class="tool-icon">📊</span>
                        <span class="tool-text">分析证据清单</span>
                    </button>
                    <button class="tool-btn" onclick="showToolDemo('图片OCR识别')">
                        <span class="tool-icon">📷</span>
                        <span class="tool-text">图片OCR识别</span>
                    </button>
                </div>

                <div class="tool-group">
                    <div class="group-title">法律查询</div>
                    <button class="tool-btn" onclick="showToolDemo('查询法条')">
                        <span class="tool-icon">📚</span>
                        <span class="tool-text">查询法条</span>
                    </button>
                    <button class="tool-btn" onclick="showToolDemo('搜索案例')">
                        <span class="tool-icon">📋</span>
                        <span class="tool-text">搜索案例</span>
                    </button>
                </div>

                <div class="tool-group">
                    <div class="group-title">智能分析</div>
                    <button class="tool-btn" onclick="showToolDemo('相似度分析')">
                        <span class="tool-icon">⚖️</span>
                        <span class="tool-text">相似度分析</span>
                    </button>
                    <button class="tool-btn" onclick="showToolDemo('判决预测')">
                        <span class="tool-icon">🔮</span>
                        <span class="tool-text">判决预测</span>
                    </button>
                    <button class="tool-btn" onclick="showToolDemo('风险评估')">
                        <span class="tool-icon">⚠️</span>
                        <span class="tool-text">风险评估</span>
                    </button>
                </div>

                <div class="tool-group">
                    <div class="group-title">费用计算</div>
                    <button class="tool-btn" onclick="showToolDemo('诉讼费用')">
                        <span class="tool-icon">💰</span>
                        <span class="tool-text">诉讼费用</span>
                    </button>
                    <button class="tool-btn" onclick="showToolDemo('律师费用')">
                        <span class="tool-icon">👨‍⚖️</span>
                        <span class="tool-text">律师费用</span>
                    </button>
                </div>
            </div>
        </aside>
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
        const state = {
            currentStep: 1,
            currentTab: 'input',
            currentResultTab: 'legal',
            caseData: {
                role: 'plaintiff',
                caseType: '',
                caseDescription: '',
                claimAmount: 0
            }
        };

        const demoData = {
            legalBasis: `
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
            similarCases: `
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
            riskAssessment: `
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
            costCalculation: `
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

        document.addEventListener('DOMContentLoaded', function() {
            initializeTabs();
            initializeResultTabs();
            initializeChat();
        });

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

        function initializeChat() {
            const chatInput = document.getElementById('chatInput');
            
            chatInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    sendMessage();
                }
            });
        }

        function sendMessage() {
            const chatInput = document.getElementById('chatInput');
            const message = chatInput.value.trim();
            
            if (!message) return;
            
            addChatMessage('user', message);
            chatInput.value = '';
            
            setTimeout(() => {
                const responses = [
                    "感谢您的咨询。根据您提供的信息，我建议您收集相关证据材料，包括借款合同、转账记录等。",
                    "您的案件情况我已了解。根据《民法典》相关规定，您可以向法院提起诉讼。",
                    "针对您的问题，建议您先确认借款合同的效力和诉讼时效问题。",
                    "本版本为演示版本，实际请连接后端服务器获取完整的AI分析服务。"
                ];
                const randomResponse = responses[Math.floor(Math.random() * responses.length)];
                addChatMessage('assistant', randomResponse);
            }, 1000);
        }

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

        function clearForm() {
            document.getElementById('caseType').value = '';
            document.getElementById('caseDescription').value = '';
            document.getElementById('claimAmount').value = '';
            state.caseData.caseType = '';
            state.caseData.caseDescription = '';
            state.caseData.claimAmount = 0;
        }

        function submitCase() {
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
            
            state.caseData.role = role;
            state.caseData.caseType = caseType;
            state.caseData.caseDescription = caseDescription;
            state.caseData.claimAmount = parseFloat(claimAmount) || 0;
            
            updateStepStatus(2, 'completed');
            updateStepStatus(3, 'completed');
            
            showToast('正在分析案件，请稍候...', 'info');
            
            setTimeout(() => {
                updateResultDisplay();
                showToast('案件分析完成', 'success');
                switchTab('result');
                
                for (let i = 4; i <= 8; i++) {
                    updateStepStatus(i, 'completed');
                }
            }, 1500);
        }

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

        function updateResultDisplay() {
            document.getElementById('resultCaseType').textContent = state.caseData.caseType || '-';
            document.getElementById('resultRole').textContent = state.caseData.role === 'plaintiff' ? '原告' : '被告';
            document.getElementById('resultAmount').textContent = state.caseData.claimAmount ? 
                `¥${state.caseData.claimAmount.toLocaleString()}` : '-';
            document.getElementById('resultWinRate').textContent = '85% - 90%';
            
            document.getElementById('legalContent').innerHTML = demoData.legalBasis;
            document.getElementById('caseContent').innerHTML = demoData.similarCases;
            document.getElementById('riskContent').innerHTML = demoData.riskAssessment;
            document.getElementById('costContent').innerHTML = demoData.costCalculation;
        }

        function showDemo() {
            document.getElementById('caseType').value = '借款合同纠纷';
            document.getElementById('caseDescription').value = '被告于2023年1月向原告借款50万元，约定月利率2%，借款期限1年。借款到期后，被告仅偿还了部分利息，本金及剩余利息至今未还。原告多次催讨未果，遂提起诉讼。';
            document.getElementById('claimAmount').value = '500000';
            
            state.caseData.caseType = '借款合同纠纷';
            state.caseData.caseDescription = document.getElementById('caseDescription').value;
            state.caseData.claimAmount = 500000;
            
            showToast('已加载演示数据', 'success');
        }

        function showToolDemo(toolName) {
            const demoContents = {
                '解析证据': '<p><strong>证据解析结果：</strong></p><p>文件：借款合同.pdf</p><p>类型：合同类证据</p><p>关键信息：</p><ul><li>借款金额：500,000元</li><li>借款期限：12个月</li><li>利率：月利率2%</li></ul>',
                '分析证据清单': '<p><strong>证据清单分析：</strong></p><p>证据数量：5项</p><p>证据充分性：<span style="color: green;">充分</span></p><p>证据链完整性：<span style="color: green;">完整</span></p>',
                '图片OCR识别': '<p><strong>OCR识别结果：</strong></p><p>识别到文字内容：借条</p><p>借款人：张三</p><p>出借人：李四</p><p>金额：五十万元整</p>',
                '查询法条': '<p><strong>查询结果：</strong></p><p>找到3条相关法条</p><p>1. 民法典第667条</p><p>2. 民法典第679条</p><p>3. 民法典第680条</p>',
                '搜索案例': '<p><strong>找到5个相似案例</strong></p><p>1. 张三诉李四借款合同纠纷案</p><p>2. 王五诉赵六民间借贷纠纷案</p><p>3. ...</p>',
                '相似度分析': '<p><strong>相似度分析结果：</strong></p><p>与典型案例1相似度：92%</p><p>与典型案例2相似度：88%</p><p>综合胜诉率：85%</p>',
                '判决预测': '<p><strong>判决预测：</strong></p><p>可能的判决结果：</p><p>1. 支持原告偿还本金请求</p><p>2. 支持原告利息请求（按合法利率计算）</p><p>3. 诉讼费用由被告承担</p>',
                '风险评估': '<p><strong>综合风险等级：</strong><span style="color: green;">低风险</span></p><p>建议提起诉讼</p>',
                '诉讼费用': '<p><strong>诉讼费用：</strong>10,500元</p><p>计算依据：《诉讼费用交纳办法》</p>',
                '律师费用': '<p><strong>律师费用估算：</strong>20,000 - 40,000元</p><p>按争议金额4%-8%计算</p>'
            };
            
            showModal(toolName, demoContents[toolName] || '演示内容');
        }

        function showModal(title, content) {
            document.getElementById('modalTitle').textContent = title;
            document.getElementById('modalBody').innerHTML = content;
            document.getElementById('modalOverlay').classList.add('active');
        }

        function closeModal() {
            document.getElementById('modalOverlay').classList.remove('active');
        }

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

        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        function toggleFullscreen() {
            if (!document.fullscreenElement) {
                document.documentElement.requestFullscreen();
            } else {
                document.exitFullscreen();
            }
        }

        function resetWorkspace() {
            if (confirm('确定要新建案件吗？当前数据将被清除。')) {
                clearForm();
                
                for (let i = 1; i <= 10; i++) {
                    updateStepStatus(i, i === 1 ? 'active' : 'pending');
                }
                
                document.getElementById('resultCaseType').textContent = '-';
                document.getElementById('resultRole').textContent = '-';
                document.getElementById('resultAmount').textContent = '-';
                document.getElementById('resultWinRate').textContent = '-';
                document.getElementById('legalContent').innerHTML = '<p>暂无数据，请先进行案件分析或点击"演示数据"查看示例</p>';
                document.getElementById('caseContent').innerHTML = '<p>暂无数据，请先进行案件分析或点击"演示数据"查看示例</p>';
                document.getElementById('riskContent').innerHTML = '<p>暂无数据，请先进行案件分析或点击"演示数据"查看示例</p>';
                document.getElementById('costContent').innerHTML = '<p>暂无数据，请先进行案件分析或点击"演示数据"查看示例</p>';
                
                switchTab('input');
                showToast('工作区已重置', 'success');
            }
        }

        document.getElementById('modalOverlay').addEventListener('click', function(e) {
            if (e.target === this) {
                closeModal();
            }
        });
    </script>
</body>
</html>

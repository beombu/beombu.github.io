---
title: "MCP 서버 비교"
categories:
  - ai
layout: single
---

<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MCP 서버 비교</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 20px;
            min-height: 100vh;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }

        h1 {
            text-align: center;
            color: #2d3748;
            margin-bottom: 40px;
            font-size: 2.5em;
        }

        .comparison-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin: 30px 0;
        }

        .card {
            border-radius: 15px;
            padding: 30px;
            color: white;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }

        .card.wrong {
            background: linear-gradient(135deg, #fc8181 0%, #f56565 100%);
        }

        .card.correct {
            background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
        }

        .card h2 {
            font-size: 1.8em;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .card .description {
            font-size: 1.1em;
            margin-bottom: 20px;
            opacity: 0.95;
            line-height: 1.6;
        }

        .features {
            background: rgba(255,255,255,0.15);
            border-radius: 10px;
            padding: 20px;
            backdrop-filter: blur(10px);
        }

        .features ul {
            list-style: none;
        }

        .features li {
            padding: 8px 0;
            padding-left: 25px;
            position: relative;
            line-height: 1.6;
        }

        .wrong .features li:before {
            content: "✗";
            position: absolute;
            left: 0;
            font-weight: bold;
            color: #fff5f5;
        }

        .correct .features li:before {
            content: "✓";
            position: absolute;
            left: 0;
            font-weight: bold;
            color: #c6f6d5;
        }

        .code-block {
            background: #2d3748;
            color: #e2e8f0;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            overflow-x: auto;
            font-family: 'Courier New', monospace;
        }

        .code-block pre {
            margin: 0;
        }

        .alert {
            background: #fff5f5;
            border: 3px solid #fc8181;
            border-radius: 15px;
            padding: 25px;
            margin: 30px 0;
        }

        .alert h2 {
            color: #c53030;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .alert p {
            color: #2d3748;
            line-height: 1.8;
            font-size: 1.1em;
        }

        .info {
            background: #ebf8ff;
            border: 3px solid #4299e1;
            border-radius: 15px;
            padding: 25px;
            margin: 30px 0;
        }

        .info h2 {
            color: #2c5282;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .info p {
            color: #2d3748;
            line-height: 1.8;
            font-size: 1.1em;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin: 30px 0;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        th {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            text-align: left;
            font-size: 1.1em;
        }

        td {
            padding: 20px;
            border-bottom: 1px solid #e2e8f0;
        }

        tr:last-child td {
            border-bottom: none;
        }

        tr:hover {
            background: #f7fafc;
        }

        .architecture {
            background: #f7fafc;
            border-radius: 15px;
            padding: 30px;
            margin: 30px 0;
        }

        .architecture h3 {
            color: #2d3748;
            margin-bottom: 20px;
            font-size: 1.5em;
        }

        .flow {
            background: white;
            padding: 20px;
            border-radius: 10px;
            border-left: 4px solid #667eea;
            margin: 15px 0;
        }

        @media (max-width: 768px) {
            .comparison-grid {
                grid-template-columns: 1fr;
            }

            .container {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
<div class="container">
    <h1>🔍 현재 코드 vs 진짜 MCP 서버</h1>

    <div class="alert">
        <h2>🚨 중요한 사실</h2>
        <p>
            <strong>제가 작성한 코드는 MCP 서버가 아닙니다!</strong><br><br>
            그냥 일반적인 Express.js REST API 서버입니다. MCP (Model Context Protocol) 표준을 전혀 따르지 않습니다.<br>
            "MCP 서버"라는 이름은 잘못된 명명이며, 정확히는 <strong>"GitLab AI Review Server"</strong> 또는 <strong>"Code Review API Server"</strong>라고 불러야 합니다.
        </p>
    </div>

    <div class="comparison-grid">
        <div class="card wrong">
            <h2>❌ 현재 구현 (일반 REST API)</h2>
            <div class="description">
                Express.js 기반의 일반적인 웹 서버
            </div>
            <div class="features">
                <ul>
                    <li>HTTP POST /review-mr 엔드포인트</li>
                    <li>JSON request/response</li>
                    <li>MCP 프로토콜 없음</li>
                    <li>JSON-RPC 없음</li>
                    <li>표준화된 인터페이스 없음</li>
                    <li>CI/CD에서 직접 호출</li>
                </ul>
            </div>
        </div>

        <div class="card correct">
            <h2>✅ 진짜 MCP 서버</h2>
            <div class="description">
                Anthropic의 Model Context Protocol 표준 구현
            </div>
            <div class="features">
                <ul>
                    <li>JSON-RPC 2.0 프로토콜</li>
                    <li>Tools, Resources, Prompts 제공</li>
                    <li>표준화된 메시지 형식</li>
                    <li>stdio/SSE/HTTP 전송</li>
                    <li>Claude Desktop 통합</li>
                    <li>AI가 직접 호출 가능</li>
                </ul>
            </div>
        </div>
    </div>

    <h2 style="margin-top: 50px; color: #2d3748; border-bottom: 3px solid #667eea; padding-bottom: 10px;">📊 상세 비교</h2>

    <table>
        <thead>
        <tr>
            <th>특성</th>
            <th>현재 코드</th>
            <th>진짜 MCP 서버</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <td><strong>프로토콜</strong></td>
            <td>HTTP REST API</td>
            <td>JSON-RPC 2.0</td>
        </tr>
        <tr>
            <td><strong>통신 방식</strong></td>
            <td>HTTP POST</td>
            <td>stdio, SSE, HTTP</td>
        </tr>
        <tr>
            <td><strong>메시지 형식</strong></td>
            <td>자유 형식 JSON</td>
            <td>표준화된 JSON-RPC</td>
        </tr>
        <tr>
            <td><strong>호출 주체</strong></td>
            <td>GitLab CI/CD</td>
            <td>Claude AI</td>
        </tr>
        <tr>
            <td><strong>표준 준수</strong></td>
            <td>없음 (커스텀 API)</td>
            <td>MCP 스펙 준수</td>
        </tr>
        <tr>
            <td><strong>통합 방식</strong></td>
            <td>Webhook / 직접 호출</td>
            <td>Claude Desktop 설정</td>
        </tr>
        </tbody>
    </table>

    <div class="architecture">
        <h3>🏗️ 아키텍처 차이</h3>

        <div class="flow" style="border-left-color: #fc8181;">
            <strong style="color: #c53030;">현재 코드 (일반 REST API):</strong>
            <div class="code-block"><pre>GitLab CI/CD
    ↓ (HTTP POST)
일반 REST API 서버 (Express.js)
    ↓
GitLab API ← 파일 조회
    ↓
Gemini API ← 리뷰 요청
    ↓
GitLab API ← 댓글 작성</pre></div>
        </div>

        <div class="flow" style="border-left-color: #48bb78;">
            <strong style="color: #2f855a;">진짜 MCP 서버:</strong>
            <div class="code-block"><pre>Claude Desktop/API
    ↓ (JSON-RPC)
MCP 서버
    ↓
Tools 제공 (review_code, get_file 등)
    ↑
Claude가 필요할 때 도구 호출
    ↓
결과를 Claude에게 반환</pre></div>
        </div>
    </div>

    <h2 style="margin-top: 50px; color: #2d3748; border-bottom: 3px solid #667eea; padding-bottom: 10px;">💻 코드 비교</h2>

    <h3 style="color: #2d3748; margin-top: 30px;">❌ 현재 코드 (일반 REST API)</h3>
    <div class="code-block"><pre>const express = require('express');
const app = express();

// 일반 HTTP 엔드포인트
app.post('/review-mr', async (req, res) => {
  const { project_id, mr_iid, gitlab_token } = req.body;

  // 직접 처리
  const result = await reviewMergeRequest(...);

  // 일반 JSON 응답
  res.json({ success: true, result });
});

app.listen(3001);</pre></div>

    <h3 style="color: #2d3748; margin-top: 30px;">✅ 진짜 MCP 서버</h3>
    <div class="code-block"><pre>import { Server } from '@modelcontextprotocol/sdk/server/index.js';
import { StdioServerTransport } from '@modelcontextprotocol/sdk/server/stdio.js';

const server = new Server({
  name: 'gitlab-review-mcp',
  version: '1.0.0'
}, {
  capabilities: {
    tools: {}
  }
});

// MCP Tool 등록
server.setRequestHandler('tools/list', async () => ({
  tools: [{
    name: 'review_merge_request',
    description: 'Review a GitLab merge request',
    inputSchema: {
      type: 'object',
      properties: {
        project_id: { type: 'string' },
        mr_iid: { type: 'string' }
      }
    }
  }]
}));

// Tool 실행 핸들러
server.setRequestHandler('tools/call', async (request) => {
  if (request.params.name === 'review_merge_request') {
    const result = await reviewMergeRequest(request.params.arguments);
    return {
      content: [{
        type: 'text',
        text: JSON.stringify(result)
      }]
    };
  }
});

// stdio 전송
const transport = new StdioServerTransport();
await server.connect(transport);</pre></div>

    <div class="info">
        <h2>ℹ️ 그럼 뭐가 필요한가요?</h2>
        <p>
            <strong>현재 상황:</strong><br>
            • GitLab CI/CD가 코드를 자동으로 리뷰하는 시스템<br>
            • 일반 REST API 서버로 충분함<br>
            • MCP 프로토콜 불필요<br><br>

            <strong>MCP가 필요한 경우:</strong><br>
            • Claude Desktop/API와 통합하고 싶을 때<br>
            • Claude가 직접 GitLab 도구를 사용하게 하고 싶을 때<br>
            • 사용자가 Claude와 대화하면서 MR을 리뷰받고 싶을 때<br>
            • 예: "Claude, 내 MR #45를 리뷰해줘" → Claude가 MCP 서버의 도구 호출<br><br>

            <strong>결론:</strong><br>
            현재 용도(CI/CD 자동 리뷰)라면 <strong>일반 REST API가 더 적합</strong>합니다!
        </p>
    </div>

    <h2 style="margin-top: 50px; color: #2d3748; border-bottom: 3px solid #667eea; padding-bottom: 10px;">🎯 올바른 명명</h2>

    <div style="background: #f7fafc; padding: 25px; border-radius: 15px; margin: 20px 0;">
        <h3 style="color: #2d3748; margin-bottom: 15px;">현재 코드는 이렇게 불러야 합니다:</h3>
        <ul style="list-style: none; padding-left: 0;">
            <li style="padding: 10px; background: white; margin: 10px 0; border-radius: 8px; border-left: 4px solid #48bb78;">
                ✅ <strong>GitLab AI Code Review Server</strong>
            </li>
            <li style="padding: 10px; background: white; margin: 10px 0; border-radius: 8px; border-left: 4px solid #48bb78;">
                ✅ <strong>Code Review API Service</strong>
            </li>
            <li style="padding: 10px; background: white; margin: 10px 0; border-radius: 8px; border-left: 4px solid #48bb78;">
                ✅ <strong>GitLab Review Webhook Server</strong>
            </li>
            <li style="padding: 10px; background: #fff5f5; margin: 10px 0; border-radius: 8px; border-left: 4px solid #fc8181;">
                ❌ <strong>MCP Server</strong> (잘못된 명명)
            </li>
        </ul>
    </div>
</div>
</body>
</html>
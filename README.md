<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>2026학년도 2학기 학교생활기록부 점검 (PDF 지원)</title>
  <!-- PDF 텍스트 추출 라이브러리 (PDF.js CDN) -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
  <script>
    // PDF.js 워커 설정
    pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
  </script>
  <style>
    :root {
      --primary: #1e40af;
      --primary-light: #3b82f6;
      --primary-dark: #1e3a8a;
      --success: #059669;
      --danger: #dc2626;
      --warning: #d97706;
      --border: #e2e8f0;
      --text-dark: #0f172a;
      --text-muted: #64748b;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Pretendard", "Segoe UI", Roboto, sans-serif;
    }

    body {
      background-color: #f1f5f9;
      color: var(--text-dark);
      line-height: 1.6;
    }

    /* 네비게이션 */
    header.navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 16px 40px;
      border-bottom: 1px solid var(--border);
      position: sticky;
      top: 0;
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(8px);
      z-index: 100;
    }
    .logo {
      font-size: 18px;
      font-weight: 800;
      color: var(--primary-dark);
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .badge-pdf {
      background: #fee2e2;
      color: #b91c1c;
      padding: 2px 8px;
      border-radius: 6px;
      font-size: 11px;
      font-weight: 700;
    }
    .btn-cta {
      background: var(--primary-dark);
      color: white;
      text-decoration: none;
      padding: 8px 18px;
      border-radius: 8px;
      font-size: 14px;
      font-weight: 600;
    }

    /* Hero */
    .hero {
      padding: 40px 20px 24px;
      text-align: center;
      background: radial-gradient(circle at top, #eff6ff 0%, #f1f5f9 80%);
    }
    .badge-hero {
      display: inline-block;
      background: #dbeafe;
      color: var(--primary-dark);
      font-size: 13px;
      font-weight: 700;
      padding: 4px 14px;
      border-radius: 9999px;
      margin-bottom: 12px;
    }
    .hero h1 {
      font-size: 32px;
      font-weight: 800;
      letter-spacing: -0.02em;
      margin-bottom: 8px;
    }
    .hero p {
      font-size: 15px;
      color: var(--text-muted);
      max-width: 750px;
      margin: 0 auto;
    }

    /* 메인 컨테이너 */
    .container {
      max-width: 1140px;
      margin: 0 auto;
      padding: 16px 20px 80px;
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    /* 상단 배너 */
    .header-card {
      background: linear-gradient(135deg, #2563eb, #1e3a8a);
      color: white;
      padding: 24px 28px;
      border-radius: 14px;
      box-shadow: 0 4px 12px rgba(37, 99, 235, 0.15);
    }
    .badge-pill {
      background: rgba(255, 255, 255, 0.2);
      padding: 3px 12px;
      border-radius: 9999px;
      font-size: 12px;
      font-weight: 600;
      display: inline-block;
      margin-bottom: 8px;
    }
    .header-card h2 {
      font-size: 22px;
      font-weight: 700;
      margin-bottom: 6px;
    }
    .header-meta {
      font-size: 13px;
      color: #cbd5e1;
    }

    /* 파일 업로드 드롭존 */
    .upload-zone {
      background: white;
      border: 2px dashed #93c5fd;
      border-radius: 12px;
      padding: 30px;
      text-align: center;
      cursor: pointer;
      transition: all 0.2s ease;
    }
    .upload-zone:hover {
      background: #eff6ff;
      border-color: #2563eb;
    }
    .upload-zone input { display: none; }
    .upload-icon { font-size: 36px; margin-bottom: 6px; }
    .upload-title { font-size: 16px; font-weight: 700; color: var(--primary-dark); }
    .upload-desc { font-size: 13px; color: var(--text-muted); margin-top: 4px; }
    .status-analyzing {
      display: none;
      color: #2563eb;
      font-weight: 700;
      margin-top: 8px;
    }

    /* 알림 배너 */
    .alert-banner {
      background: #fffbeb;
      border: 1px solid #fcd34d;
      border-radius: 12px;
      padding: 16px 20px;
      display: flex;
      gap: 14px;
      align-items: flex-start;
    }
    .alert-title {
      font-size: 14px;
      font-weight: 700;
      color: #92400e;
      display: flex;
      align-items: center;
      gap: 8px;
      margin-bottom: 4px;
    }
    .alert-badge {
      background: white;
      border: 1px solid #f59e0b;
      color: #b45309;
      padding: 1px 8px;
      border-radius: 9999px;
      font-size: 11.5px;
    }
    .alert-desc {
      font-size: 13.5px;
      color: #b45309;
    }

    /* 수치 카드 */
    .summary-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 12px;
    }
    .summary-card {
      background: white;
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 16px 20px;
    }
    .summary-card .label { font-size: 12.5px; color: var(--text-muted); margin-bottom: 4px; }
    .summary-card .value { font-size: 24px; font-weight: 800; display: flex; align-items: baseline; gap: 2px; }
    .summary-card .value span { font-size: 15px; font-weight: 500; }
    .val-total { color: #1e293b; }
    .val-success { color: #059669; }
    .val-danger { color: #dc2626; }
    .val-warning { color: #d97706; }

    /* 테이블 */
    .content-box {
      background: white;
      border-radius: 12px;
      border: 1px solid var(--border);
      overflow: hidden;
    }
    .table-container { padding: 20px; }
    .section-title {
      font-size: 15px;
      font-weight: 700;
      color: var(--primary-dark);
      display: flex;
      align-items: center;
      gap: 8px;
      margin-bottom: 14px;
    }
    .section-title::before {
      content: "";
      width: 4px;
      height: 14px;
      background: #2563eb;
      border-radius: 2px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 13px;
    }
    th, td {
      padding: 12px 14px;
      text-align: left;
      border-bottom: 1px solid var(--border);
      vertical-align: top;
    }
    th {
      background-color: #f8fafc;
      color: var(--text-muted);
      font-weight: 600;
    }
    .td-num { width: 50px; text-align: center; color: var(--text-muted); font-weight: 700; }

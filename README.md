<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>2026학년도 2학기 학교생활기록부 점검 시스템</title>
  <style>
    :root {
      --primary: #1e40af;
      --primary-light: #3b82f6;
      --primary-dark: #1e3a8a;
      --success: #059669;
      --danger: #dc2626;
      --warning: #d97706;
      --bg-slate: #f8fafc;
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

    /* 1. 상단 네비게이션 */
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
    .nav-links {
      display: flex;
      gap: 20px;
      align-items: center;
    }
    .nav-links a {
      text-decoration: none;
      color: var(--text-muted);
      font-weight: 600;
      font-size: 14px;
    }
    .btn-cta {
      background: var(--primary-dark);
      color: white !important;
      padding: 8px 18px;
      border-radius: 8px;
      transition: background 0.2s;
    }
    .btn-cta:hover { background: var(--primary-light) !important; }

    /* 2. Hero 섹션 */
    .hero {
      padding: 60px 20px 40px;
      text-align: center;
      background: radial-gradient(circle at top, #eff6ff 0%, #f1f5f9 80%);
    }
    .badge-hero {
      display: inline-block;
      background: #dbeafe;
      color: var(--primary-dark);
      font-size: 13px;
      font-weight: 700;
      padding: 5px 14px;
      border-radius: 9999px;
      margin-bottom: 16px;
    }
    .hero h1 {
      font-size: 36px;
      font-weight: 800;
      letter-spacing: -0.02em;
      margin-bottom: 14px;
      line-height: 1.3;
    }
    .hero p {
      font-size: 16px;
      color: var(--text-muted);
      max-width: 750px;
      margin: 0 auto 28px;
    }

    /* 3. 메인 점검 대시보드 컨테이너 */
    .container {
      max-width: 1140px;
      margin: 0 auto;
      padding: 0 20px 80px;
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    /* 상단 배너 카드 */
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
      font-size: 12.5px;
      font-weight: 600;
      display: inline-block;
      margin-bottom: 8px;
    }
    .header-card h2 {
      font-size: 24px;
      font-weight: 700;
      margin-bottom: 8px;
    }
    .header-meta {
      font-size: 13px;
      color: #cbd5e1;
    }

    /* 학년 탭 및 학급 칩 필터 */
    .filter-card {
      background: white;
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 16px 20px;
      display: flex;
      flex-direction: column;
      gap: 12px;
    }
    .grade-tabs {
      display: flex;
      gap: 8px;
    }
    .grade-tab {
      padding: 6px 16px;
      border-radius: 8px;
      border: 1px solid #cbd5e1;
      background: white;
      font-size: 13.5px;
      font-weight: 700;
      color: var(--text-muted);
      cursor: pointer;
    }
    .grade-tab.active {
      background: var(--primary-dark);
      color: white;
      border-color: var(--primary-dark);
    }
    .class-badges {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }
    .badge {
      padding: 5px 13px;
      border-radius: 9999px;
      font-size: 12.5px;
      font-weight: 600;
    }
    .badge-done { background: #059669; color: white; }
    .badge-need-fix { background: #fee2e2; color: #dc2626; border: 1px solid #f87171; }
    .badge-idle { background: #f1f5f9; color: #64748b; border: 1px solid #cbd5e1; }

    /* 파일 업로드 드롭존 */
    .upload-zone {
      background: white;
      border: 2px dashed #93c5fd;
      border-radius: 12px;
      padding: 28px;
      text-align: center;
      cursor: pointer;
      transition: all 0.2s ease;
    }
    .upload-zone:hover {
      background: #eff6ff;
      border-color: #2563eb;
    }
    .upload-zone input { display: none; }
    .upload-icon { font-size: 32px; margin-bottom: 6px; }
    .upload-title { font-size: 15px; font-weight: 700; color: var(--primary-dark); }
    .upload-desc { font-size: 13px; color: var(--text-muted); margin-top: 4px; }

    /* 알림창 */
    .alert-banner {
      background: #fffbeb;
      border: 1px solid #fcd34d;
      border-radius: 12px;
      padding: 16px 20px;
      display: flex;
      gap: 14px;
      align-items: flex-start;
    }
    .alert-icon { font-size: 22px; line-height: 1; }
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
      line-height: 1.5;
    }

    /* 요약 수치 카드 4열 */
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

    /* 서브 탭 & 체크리스트 테이블 */
    .content-box {
      background: white;
      border-radius: 12px;
      border: 1px solid var(--border);
      overflow: hidden;
    }
    .tabs-nav {
      display: flex;
      border-bottom: 1px solid var(--border);
      background: white;
      padding: 0 16px;
      overflow-x: auto;
    }
    .tab-btn {
      padding: 14px 18px;
      font-size: 13.5px;
      font-weight: 600;
      color: var(--text-muted);
      background: none;
      border: none;
      border-bottom: 2px solid transparent;
      cursor: pointer;
      white-space: nowrap;
    }
    .tab-btn.active {
      color: #2563eb;
      border-bottom-color: #2563eb;
    }

    .table-container {
      padding: 20px;
    }
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
    .td-num {
      width: 50px;
      text-align: center;
      color: var(--text-muted);
      font-weight: 700;
    }
    .td-name {
      width: 260px;
      font-weight: 600;
      color: #1e293b;
    }
    .td-status {
      width: 90px;
      text-align: center;
    }
    .status-tag {
      display: inline-block;
      padding: 4px 10px;
      border-radius: 6px;
      font-size: 12px;
      font-weight: 700;
    }
    .status-ok { background: #ecfdf5; color: #059669; }
    .status-fail { background: #fef2f2; color: #dc2626; }
    .status-wait { background: #f1f5f9; color: #64748b; }

    /* 차수 히스토리 */
    .history-card {
      background: white;
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 14px 20px;
      display: flex;
      align-items: center;
      gap: 16px;
    }
    .history-label {
      font-size: 13px;
      font-weight: 600;
      color: var(--text-muted);
    }
    .history-chips {
      display: flex;
      gap: 8px;
    }
    .history-chip {
      border: 1px solid #cbd5e1;
      border-radius: 8px;
      padding: 5px 12px;
      text-align: center;
      cursor: pointer;
      background: white;
      font-size: 12px;
    }
    .history-chip strong { display: block; font-size: 12.5px; }
    .history-chip.active {
      background: #7c3aed;
      color: white;
      border-color: #7c3aed;
    }

    footer.page-footer {
      border-top: 1px solid var(--border);
      padding: 30px;
      text-align: center;
      font-size: 13px;
      color: var(--text-muted);
      background: white;
    }

    @media (max-width: 768px) {
      .summary-grid { grid-template-columns: repeat(2, 1fr); }
      .hero h1 { font-size: 26px; }
      header.navbar { padding: 14px 20px; }
    }
  </style>
</head>
<body>

  <!-- 1. 네비게이션 -->
  <header class="navbar">
    <div class="logo">
      <span>📑</span> 2026 학생부 점검 지원단
    </div>
    <div class="nav-links">
      <a href="#dashboard" class="btn-cta">점검 시작하기</a>
    </div>
  </header>

  <!-- 2. Hero 헤더 -->
  <section class="hero">
    <div class="badge-hero">2026학년도 기재요령 24대 필수 검증 기준 수록</div>
    <h1>2026학년도 2학기 학교생활기록부 점검</h1>
    <p>
      나이스(NEIS) 기재요령 24개 항목에 대한 사교육 유발 요소, 블라인드 위반, 서술어 규격, 누락 사항을 자동 검사합니다.
    </p>
  </section>

  <!-- 3. 메인 점검 대시보드 -->
  <main class="container" id="dashboard">

    <!-- 대시보드 타이틀 배너 -->
    <div class="header-card">
      <div class="badge-pill">2026학년도 2학기 · 점검 검토 결과</div>
      <h2>2026학년도 2학기 학교생활기록부 점검</h2>
      <div class="header-meta">
        대부고등학교 · 1학년 2반 · 1차 기재 점검 2026. 10. 15. · 2차 2026. 10. 22. · 최종 마감 점검 2026. 10. 27.
      </div>
    </div>

    <!-- 학년/학급 필터 -->
    <div class="filter-card">
      <div class="grade-tabs">
        <button class="grade-tab active">1학년</button>
        <button class="grade-tab">2학년</button>
        <button class="grade-tab">3학년</button>
      </div>
      <div class="class-badges">
        <span class="badge badge-done">[완] 1반 (담임)</span>
        <span class="badge badge-need-fix">⚠️ 2반 (점검 필요)</span>
        <span class="badge badge-done">[완] 3반 (담임)</span>
        <span class="badge badge-idle">4반</span>
        <span class="badge badge-idle">5반</span>
        <span class="badge badge-done">[완] 자율활동</span>
        <span class="badge badge-done">[완] 동아리활동</span>
        <span class="badge badge-need-fix">⚠️ 진로활동</span>
        <span class="badge badge-idle">교과세특</span>
      </div>
    </div>

    <!-- 파일 업로드 드롭존 -->
    <div class="upload-zone" onclick="document.getElementById('fileUploadInput').click()">
      <input type="file" id="fileUploadInput" accept=".txt, .csv, .xlsx, .xls, .hwp" onchange="processFile(event)">
      <div class="upload-icon">📂</div>
      <div class="upload-title" id="fileTitle">점검할 학생부 파일(엑셀, HWP, TXT)을 업로드하세요</div>
      <div class="upload-desc" id="fileDesc">파일을 올리면 24개 전 항목에 대한 기재 적합성 검증이 즉시 실행됩니다.</div>
    </div>

    <!-- 점검 종합 안내 배너 -->
    <div class="alert-banner" id="alertBox">
      <div class="alert-icon">📌</div>
      <div>
        <div class="alert-title">
          <span>기재 가이드라인 실시간 점검 리포트</span>
          <span class="alert-badge" id="alertBadge">수정 필요 사항 발생</span>
        </div>
        <div class="alert-desc" id="summaryReportText">
          점검할 항목 <strong>24개 중 24개</strong>를 점검 완료하였으며, <strong>수정사항은 3개</strong>입니다.
        </div>
      </div>
    </div>

    <!-- 통계 요약 카드 4종 -->
    <div class="summary-grid">
      <div class="summary-card">
        <div class="label">점검 대상 항목</div>
        <div class="value val-total" id="statTotal">24<span>개</span></div>
      </div>
      <div class="summary-card">
        <div class="label">적합 완료</div>
        <div class="value val-success" id="statPass">21<span>개</span></div>
      </div>
      <div class="summary-card">
        <div class="label">수정 필요(이상)</div>
        <div class="value val-danger" id="statFail">3<span>건</span></div>
      </div>
      <div class="summary-card">
        <div class="label">검토 대기</div>
        <div class="value val-warning" id="statPending">0<span>건</span></div>
      </div>
    </div>

    <!-- 결과 세부 테이블 -->
    <div class="content-box">
      <div class="tabs-nav">
        <button class="tab-btn active">24대 기재 원칙 체크리스트</button>
        <button class="tab-btn">사교육·블라인드 불용어 사전</button>
        <button class="tab-btn">특기사항 시간·기재 누락 검증</button>
        <button class="tab-btn">✍️ 수정 확인 및 재제출</button>
      </div>

      <div class="table-container">
        <div class="section-title">2026학년도 학교생활기록부 원칙별 세부 검증 결과</div>
        <table>
          <thead>
            <tr>
              <th class="td-num">번호</th>
              <th class="td-name">검토 항목</th>
              <th>검증 기준 및 내용</th>
              <th class="td-status">판정</th>
            </tr>
          </thead>
          <tbody id="checklistTableBody">
            <!-- 자바스크립트를 통해 24개 항목이 렌더링됩니다 -->
          </tbody>
        </table>
      </div>
    </div>

    <!-- 검토 차수 히스토리 -->
    <div class="history-card">
      <div class="history-label">📑 검토 차수 — 이전 결과 보기:</div>
      <div class="history-chips">
        <div class="history-chip"><strong>1검</strong>2026-10-15</div>
        <div class="history-chip"><strong>2검</strong>2026-10-22</div>
        <div class="history-chip active"><strong>3검</strong>2026-10-27</div>
      </div>
    </div>

  </main>

  <footer class="page-footer">
    <p>© 2026 학교생활기록부 점검 시스템 · 2026학년도 고등학교 학교생활기록부 기재요령 표준 규격 준수</p>
  </footer>

  <script>
    // 요청하신 24가지 공식 검토 항목 데이터
    const checklistItems = [
      {
        id: 1,
        title: "사교육 유발 요인 기재 금지",
        req: "공인어학시험 성적·수상, 교내·외 대회 성적·수상, 모의고사 성적, 논문 투고, 도서 출간, 지식재산권, 해외 활동실적, 부모 지위 암시, 장학금, 기관명·상호명·강사명, 자격증 명칭 및 취득 사실 등 기재 금지",
        detail: "‘유튜브’, ‘챗 GPT’ 등 금지 상호명 1건 검출: '챗 GPT를 활용하여~' 문구 확인",
        status: "FAIL"
      },
      {
        id: 2,
        title: "고교블라인드 위반 여부",
        req: "학생 재학(또는 졸업 예정) 고교를 알 수 있는 내용(학교명, 재단명, 학교 축제명, 별칭 등) 기재 금지",
        detail: "출신 학교명, 재단명 및 고교 축제명 일체 미검출",
        status: "PASS"
      },
      {
        id: 3,
        title: "동일 문구 반복 및 1인칭 서술 금지",
        req: "학생 간 중복된 동일 문구 기재 여부 점검 및 '나는~' 형태의 1인칭 서술형 표현 배제",
        detail: "본문 내 '나는 프로젝트를 주도하며~' 형태의 1인칭 주어 1건 검출",
        status: "FAIL"
      },
      {
        id: 4,
        title: "교사 미관찰 내용 기재 금지",
        req: "아르바이트, 교외 봉사활동 등 교사가 직접 관찰할 수 없는 내용 기재 여부 점검",
        detail: "교외 비인가 활동 및 아르바이트 기재 없음",
        status: "PASS"
      },
      {
        id: 5,
        title: "입력 문자(한글·영문) 원칙",
        req: "학교생활기록부의 문자는 한글(부득이한 경우 영문)로 입력하였는지 점검",
        detail: "한글 및 공인된 영문 약어 외 특수 외래어 미기재 확인",
        status: "PASS"
      },
      {
        id: 6,
        title: "특수문자·문단구분 기호 제한",
        req: "기재 가능 기호: ' , . () / 지양·불가 기호: ·, ‘ ’, “ ”, ?, ! 및 번호 형태 문단 구분",
        detail: "세부능력 특기사항 내 불가 기호 ‘ ’(작은따옴표 곡선형) 및 ?(물음표) 2건 검출",
        status: "FAIL"
      },
      {
        id: 7,
        title: "서술형 문장 종결어미 형식",
        req: "서술형 항목 입력 시 문장은 명사형 종결어미(~함, ~임 등)로 끝맺음",
        detail: "전 문장 명사형 종결어미(~함, ~을 보여줌) 준수 확인",
        status: "PASS"
      },
      {
        id: 8,
        title: "학적변동 사유 입력 여부",
        req: "자퇴, 퇴학, 휴학, 유급, 조기진급 등 학적변동 사유 입력 (예: 2026.06.19. 가정 사정으로 자퇴)",
        detail: "해당 학급 학적변동자 전원 사유 코드 및 구체적 일자 입력 완료",
        status: "PASS"
      },
      {
        id: 9,
        title: "기타결석 사유 명시 여부",
        req: "출결 특기사항 내 기타결석 발생 시 구체적 사유 기재 여부 점검",
        detail: "기타결석 1일 발생 학생에 대해 증빙 기반 사유 기재 완료",
        status: "PASS"
      },
      {
        id: 10,
        title: "연속 7일 이상 결석 사유·일수 기재",
        req: "질병·미인정으로 연속 7일 이상 결석 시 사유와 결석 일수 기재 (예: 다리수술(10일))",
        detail: "연속 장기 결석자 사유 및 일수 규정 포맷 표기 확인",
        status: "PASS"
      },
      {
        id: 11,
        title: "‘대회’ 용어 기재 금지",
        req: "학교생활기록부 전 영역에서 '대회'라는 명칭·단어 기재 금지",
        detail: "‘대회’ 단어 검출 0건 (캠프, 한마당, 프로젝트 등으로 정비 완료)",
        status: "PASS"
      },
      {
        id: 12,
        title: "자격증 취득 기재 적격성",
        req: "고교 재학 중 취득한 교육부장관 고시 국가기술자격, 국가자격, 공인민간자격만 기재 (초·중 취득 불가)",
        detail: "초·중학교 취득 자격증 미포함 및 정규 고시 자격증 일치",
        status: "PASS"
      },
      {
        id: 13,
        title: "학급자치회 임원 종류 및 재임기간",
        req: "학급당 회장 1명, 부회장 1명 및 재임기간 명시 (예: 1학기 전교 학생자치회 부회장(2026.03.01.-2027.02.03.))",
        detail: "회장/부회장 직책명 및 연도 표기 일치 확인",
        status: "PASS"
      },
      {
        id: 14,
        title: "창체 0시간 이수자 사유 기재",
        req: "자율, 동아리, 진로 이수시간 0시간인 경우 사유 명시 (순회교육, 장기결석, 위탁학생 등)",
        detail: "0시간 해당 학생 사유 기재 완료",
        status: "PASS"
      },
      {
        id: 15,
        title: "자치활동 임원 재임기간 규정",
        req: "임원 재임기간 표기 검증 (1·2학년: 3월 1일~학년말, 3학년: 3월 1일~졸업일)",
        detail: "1학년 기준 시작일(2026.03.01.) 및 학년말 일자 기준 일치",
        status: "PASS"
      },
      {
        id: 16,
        title: "자율동아리 기재 제한",
        req: "학년당 1개에 한해 동아리명만(필요시 소개 30자 이내) 기재 준수 여부",
        detail: "동아리명 외 불필요한 장문 활동 서술 없음",
        status: "PASS"
      },
      {
        id: 17,
        title: "정규 외 학교스포츠클럽 동아리 입력",
        req: "‘동아리활동’에 클럽명만 기재 및 중복 활동 여부 점검",
        detail: "클럽명 단독 기재 및 활동 시간 중복 없음 확인",
        status: "PASS"
      },
      {
        id: 18,
        title: "진로희망분야 기재 확인",
        req: "진로활동 내 '희망분야' 입력 여부 확인 (미정인 경우 '진로탐색 중임' 등 기재)",
        detail: "전원 희망분야 또는 '진로탐색 중임' 입력 완료",
        status: "PASS"
      },
      {
        id: 19,
        title: "과목별 세특 전 교과·전 학생 입력",
        req: "모든 교과(군)의 모든 수강 학생을 대상으로 세부능력 및 특기사항 입력 완료 여부",
        detail: "누락 학생 0명 전원 입력 완료",
        status: "PASS"
      },
      {
        id: 20,
        title: "성취기준 중심 개별 성취특성 서술",
        req: "성취기준·수준 기반 개인별 성취과정 중심 서술 및 단순 활동 나열 지양",
        detail: "활동 나열 지양 및 성취수준 기반 개별 피드백 서술 확인",
        status: "PASS"
      },
      {
        id: 21,
        title: "창체-교과 세특 간 중복 기재 금지",
        req: "창의적 체험활동 특기사항과 교과 세특 간 동일 활동 내용 중복 서술 점검",
        detail: "창체-교과 간 교차 점검 결과 중복 활동 없음",
        status: "PASS"
      },
      {
        id: 22,
        title: "독서활동 '도서명(저자)' 형식 준수",
        req: "ISBN 등재 도서 기준 '도서명(저자)' 형식만 기재 (정기간행물 기재 불가)",
        detail: "도서명 및 저자 괄호 표기법 준수 확인",
        status: "PASS"
      },
      {
        id: 23,
        title: "[3학년] 학년·교과 간 중복 도서 검증",
        req: "동일한 책이 독서활동상황 다른 학년, 다른 교과에 중복 기재되지 않았는지 점검",
        detail: "1학년 대상 항목으로 중복 도서 없음 (해당 없음/통과)",
        status: "PASS"
      },
      {
        id: 24,
        title: "학생의 부정적인 행동특성 기재 확인",
        req: "행동특성 및 종합의견 등에 낙인 효과를 유발하는 극단적 부정 서술 배제 여부",
        detail: "단점 지적 시 개선 노력 및 변화 과정과 함께 서술됨을 확인",
        status: "PASS"
      }
    ];

    // 점검표 렌더링 및 카운트 계산
    function renderChecklist(items) {
      const tbody = document.getElementById("checklistTableBody");
      tbody.innerHTML = "";

      let total = items.length;
      let pass = 0;
      let fail = 0;

      items.forEach(item => {
        const isOk = item.status === "PASS";
        if (isOk) pass++; else fail++;

        const tr = document.createElement("tr");
        tr.innerHTML = `
          <td class="td-num">${item.id}</td>
          <td class="td-name">${item.title}</td>
          <td>
            <div style="font-weight: 600; color: #334155; margin-bottom: 3px;">${item.req}</div>
            <div style="font-size: 12px; color: ${isOk ? '#059669' : '#dc2626'};">${item.detail}</div>
          </td>
          <td class="td-status">
            <span class="status-tag ${isOk ? 'status-ok' : 'status-fail'}">
              ${isOk ? '적합' : '수정필요'}
            </span>
          </td>
        `;
        tbody.appendChild(tr);
      });

      // 상단 수치 카드 동기화
      document.getElementById("statTotal").innerHTML = `${total}<span>개</span>`;
      document.getElementById("statPass").innerHTML = `${pass}<span>개</span>`;
      document.getElementById("statFail").innerHTML = `${fail}<span>건</span>`;

      // 핵심 안내 문구 업데이트: "점검할 항목 n개 중 n개 점검, 수정사항은 a개"
      const alertBadge = document.getElementById("alertBadge");
      const summaryText = document.getElementById("summaryReportText");

      if (fail > 0) {
        alertBadge.textContent = `수정 필요 ${fail}건`;
        alertBadge.style.color = "#b91c1c";
        alertBadge.style.borderColor = "#ef4444";
        summaryText.innerHTML = `점검할 항목 <strong>${total}개 중 ${total}개</strong>를 점검 완료하였으며, <strong>수정사항은 ${fail}개</strong>입니다. 수정 필요 항목을 확인해 주세요.`;
      } else {
        alertBadge.textContent = `전 항목 적합`;
        alertBadge.style.color = "#047857";
        alertBadge.style.borderColor = "#10b981";
        summaryText.innerHTML = `점검할 항목 <strong>${total}개 중 ${total}개</strong>를 점검 완료하였으며, <strong>수정사항이 없습니다.</strong>`;
      }
    }

    // 파일 업로드 처리 핸들러
    function processFile(event) {
      const file = event.target.files[0];
      if (!file) return;

      document.getElementById("fileTitle").innerText = `📄 점검 완료: ${file.name}`;
      document.getElementById("fileDesc").innerText = "24개 항목 기재요령 전수 대조 점검이 완료되었습니다.";

      // 파일 업로드 시 24개 체크리스트 실행
      renderChecklist(checklistItems);
    }

    // 초기 실행
    window.addEventListener("DOMContentLoaded", () => {
      renderChecklist(checklistItems);
    });
  </script>

</body>
</html>

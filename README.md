<!doctype html>
<html lang="pt-BR">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="description" content="Sistema de Gestão de Pessoas e Demandas - Corporativo" />
    <title>Sistema de Gestão - Pessoas e Demandas</title>
    <style>
      /* ============================================== RESET E VARIÁVEIS ============================================== */
      * { margin: 0; padding: 0; box-sizing: border-box; }
      :root {
        --bg-900: #020617; --bg-800: #0b1220; --surface: #0f172a; --surface-2: #1e293b;
        --text-primary: #e6eef8; --text-secondary: #9aa6b3; --border: #22303f;
        --primary: #2563eb; --primary-strong: #1e40af; --success: #16a34a;
        --warning: #f59e0b; --danger: #ef4444; --radius: 8px;
        --color-blue: #2563eb; --color-purple: #a855f7; --color-yellow: #facc15;
        --color-green: #22c55e; --color-pink: #ec4899; --color-indigo: #6366f1;
        --color-orange: #f97316; --color-red: #ef4444; --color-teal: #14b8a6; --color-cyan: #06b6d4;
      }
      html.light-mode { --bg-900: #f8fafc; --bg-800: #f1f5f9; --surface: #ffffff; --surface-2: #e2e8f0; --text-primary: #1e293b; --text-secondary: #475569; --border: #cbd5e1; }
      /* ============================================== LAYOUT BASE ============================================== */
      html, body { height: 100%; }
      body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; background: linear-gradient(135deg, var(--bg-900), var(--bg-800), var(--bg-900)); color: var(--text-primary); -webkit-font-smoothing: antialiased; }
      /* ============================================== HEADER ============================================== */
      header { background: linear-gradient(180deg, rgba(11, 18, 32, 0.7), rgba(11, 18, 32, 0.6)); backdrop-filter: blur(8px); border-bottom: 1px solid var(--border); position: sticky; top: 0; z-index: 40; }
      .header-container { max-width: 1800px; margin: 0 auto; padding: 12px 16px; }
      .header-top { display: flex; align-items: center; justify-content: space-between; gap: 16px; flex-wrap: wrap; margin-bottom: 12px; }
      .header-title { display: flex; align-items: center; gap: 12px; }
      .header-icon { padding: 6px; background: rgba(37, 99, 235, 0.12); border-radius: var(--radius); }
      .header-icon svg { width: 20px; height: 20px; color: var(--primary); display: block; }
      h1 { font-size: 1.125rem; font-weight: 700; color: var(--text-primary); }
      .header-subtitle { font-size: 0.75rem; color: var(--text-secondary); }
      .header-actions { display: flex; gap: 8px; align-items: center; }
      button { padding: 6px 12px; border-radius: var(--radius); border: 1px solid var(--border); font-size: 0.875rem; font-weight: 500; cursor: pointer; transition: all 0.16s; display: inline-flex; align-items: center; gap: 6px; background: transparent; color: var(--text-primary); }
      button:hover:not(:disabled) { border-color: var(--primary); background: rgba(37, 99, 235, 0.08); }
      button:focus { outline: none; box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.12); }
      button:disabled { opacity: 0.5; cursor: not-allowed; }
      button svg { width: 14px; height: 14px; display: block; }
      .stats-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; margin-top: 12px; }
      .stat-card { background: linear-gradient(180deg, rgba(255, 255, 255, 0.02), rgba(0, 0, 0, 0.03)); border: 1px solid rgba(255, 255, 255, 0.02); border-radius: var(--radius); padding: 12px; }
      .stat-label { font-size: 10px; text-transform: uppercase; color: var(--text-secondary); font-weight: 600; margin-bottom: 6px; }
      .stat-value { font-size: 1.25rem; font-weight: 700; color: var(--text-primary); }
      .stat-value.blue { color: var(--primary); }
      .stat-value.green { color: var(--success); }
      .stat-value.purple { color: var(--color-purple); }
      .stat-value.yellow { color: var(--color-yellow); }
      .filters { margin-top: 12px; background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 12px; display: none; }
      .filters.active { display: block; }
      .filter-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 12px; }
      .filter-group label { display: block; font-size: 0.75rem; font-weight: 600; color: var(--text-secondary); margin-bottom: 6px; }
      input, select { width: 100%; padding: 8px 12px; font-size: 0.95rem; background: transparent; border: 1px solid rgba(255, 255, 255, 0.04); border-radius: var(--radius); color: var(--text-primary); }
      input::placeholder { color: var(--text-secondary); }
      input:focus, select:focus { outline: none; border-color: var(--primary); box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.12); }
      .export-buttons-container { margin-top: 12px; padding-top: 12px; border-top: 1px solid var(--border); }
      .export-buttons-container label { display: block; font-size: 0.75rem; font-weight: 600; color: var(--text-secondary); margin-bottom: 8px; }
      .export-buttons { display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 8px; }
      .btn-export { display: inline-flex; align-items: center; justify-content: center; gap: 6px; padding: 8px 12px; font-size: 0.8rem; font-weight: 500; background: linear-gradient(135deg, rgba(37, 99, 235, 0.1), rgba(37, 99, 235, 0.05)); border: 1px solid rgba(37, 99, 235, 0.3); border-radius: var(--radius); color: var(--primary); cursor: pointer; transition: all 0.2s ease; white-space: nowrap; text-overflow: ellipsis; overflow: hidden; }
      .btn-export:hover:not(:disabled) { background: linear-gradient(135deg, rgba(37, 99, 235, 0.2), rgba(37, 99, 235, 0.12)); border-color: var(--primary); box-shadow: 0 4px 12px rgba(37, 99, 235, 0.15); transform: translateY(-2px); }
      .btn-export:active { transform: translateY(0); }
      .btn-export svg { width: 16px; height: 16px; flex-shrink: 0; }
      @media (max-width: 640px) { .export-buttons { grid-template-columns: repeat(2, 1fr); } }
      @media (max-width: 420px) { .export-buttons { grid-template-columns: 1fr; } .btn-export { font-size: 0.75rem; padding: 6px 10px; } }
      /* ============================================== MAIN CONTENT ============================================== */
      main { max-width: 1800px; margin: 0 auto; padding: 16px; min-height: calc(100vh - 200px); }
      .people-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
      @media (min-width: 640px) { .people-grid { grid-template-columns: repeat(3, 1fr); } }
      @media (min-width: 768px) { .people-grid { grid-template-columns: repeat(4, 1fr); } }
      @media (min-width: 1024px) { .people-grid { grid-template-columns: repeat(5, 1fr); } }
      .person-card { background: linear-gradient(180deg, rgba(255, 255, 255, 0.02), rgba(0, 0, 0, 0.03)); border: 1px solid var(--border); border-radius: var(--radius); padding: 16px; transition: all 0.2s; }
      .person-card:hover { border-color: var(--primary); background: linear-gradient(180deg, rgba(37, 99, 235, 0.05), rgba(37, 99, 235, 0.02)); }
      .person-header { display: flex; gap: 12px; margin-bottom: 12px; }
      .person-avatar { width: 40px; height: 40px; border-radius: 50%; background: linear-gradient(135deg, var(--primary), var(--color-purple)); display: flex; align-items: center; justify-content: center; font-weight: 700; color: white; flex-shrink: 0; }
      .person-info h3 { font-size: 1rem; font-weight: 600; color: var(--text-primary); margin-bottom: 2px; }
      .person-info p { font-size: 0.75rem; color: var(--text-secondary); }
      .demands-section { margin-top: 12px; }
      .demands-title { font-size: 0.75rem; color: var(--text-secondary); font-weight: 600; margin-bottom: 6px; }
      .demands-list { display: flex; flex-direction: column; gap: 4px; margin-bottom: 12px; }
      .demand-item { display: flex; align-items: center; gap: 6px; font-size: 0.85rem; padding: 4px 0; }
      .demand-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }
      .btn-assign { width: 100%; padding: 8px; background: rgba(37, 99, 235, 0.1); color: var(--primary); border: 1px solid rgba(37, 99, 235, 0.2); border-radius: var(--radius); font-size: 0.85rem; cursor: pointer; transition: all 0.2s; }
      .btn-assign:hover { background: rgba(37, 99, 235, 0.15); border-color: var(--primary); }
      .empty-state { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 32px; text-align: center; grid-column: 1 / -1; }
      .empty-state svg { width: 40px; height: 40px; color: var(--text-secondary); margin: 0 auto 8px; display: block; }
      .empty-state p { color: var(--text-secondary); font-size: 0.95rem; }
      /* ============================================== MODAL ============================================== */
      .modal-overlay { position: fixed; inset: 0; background: rgba(0, 0, 0, 0.5); display: none; align-items: center; justify-content: center; z-index: 90; padding: 20px; }
      .modal-overlay.active { display: flex; }
      .modal { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); width: 100%; max-width: 500px; max-height: calc(100vh - 40px); overflow-y: auto; box-shadow: 0 20px 25px rgba(0, 0, 0, 0.3); }
      .modal-header { display: flex; justify-content: space-between; align-items: center; padding: 16px; border-bottom: 1px solid var(--border); position: sticky; top: 0; background: var(--surface); }
      .modal-person { display: flex; gap: 12px; align-items: center; }
      .modal-avatar { width: 40px; height: 40px; border-radius: 50%; background: linear-gradient(135deg, var(--primary), var(--color-purple)); display: flex; align-items: center; justify-content: center; font-weight: 700; color: white; }
      .modal-name { font-weight: 600; color: var(--text-primary); }
      .modal-count { font-size: 0.85rem; color: var(--text-secondary); }
      .modal-close { width: 32px; height: 32px; padding: 0; display: flex; align-items: center; justify-content: center; }
      .modal-section { padding: 16px; }
      .modal-section-title { font-size: 0.85rem; font-weight: 600; color: var(--text-secondary); text-transform: uppercase; margin-bottom: 12px; }
      .available-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 8px; margin-bottom: 8px; }
      .available-item { background: rgba(255, 255, 255, 0.02); border: 1px solid var(--border); border-radius: 6px; padding: 10px; cursor: pointer; display: flex; align-items: center; gap: 8px; transition: all 0.14s; font-size: 0.9rem; }
      .available-item:hover:not(:disabled) { background: rgba(255, 255, 255, 0.04); border-color: rgba(37, 99, 235, 0.3); }
      .available-item:disabled { opacity: 0.5; cursor: not-allowed; }
      .assigned-badge { font-size: 11px; color: var(--success); font-weight: 700; margin-left: auto; }
      .btn-close-modal { width: 100%; padding: 10px 16px; background: var(--primary); color: white; border: none; border-radius: var(--radius); font-size: 0.95rem; font-weight: 600; cursor: pointer; margin-top: 16px; }
      .btn-close-modal:hover { background: var(--primary-strong); }
      /* Demand Colors */
      .bg-blue { background-color: var(--color-blue); } .bg-purple { background-color: var(--color-purple); } .bg-yellow { background-color: var(--color-yellow); } .bg-green { background-color: var(--color-green); } .bg-pink { background-color: var(--color-pink); } .bg-indigo { background-color: var(--color-indigo); } .bg-orange { background-color: var(--color-orange); } .bg-red { background-color: var(--color-red); } .bg-teal { background-color: var(--color-teal); } .bg-cyan { background-color: var(--color-cyan); }
      /* ============================================== TOAST NOTIFICATIONS ============================================== */
      .toast { position: fixed; bottom: 20px; right: 20px; padding: 12px 16px; background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); color: var(--text-primary); font-size: 0.95rem; z-index: 100; animation: slideIn 0.3s ease; max-width: 300px; }
      .toast.success { border-color: rgba(22, 163, 74, 0.3); background: rgba(22, 163, 74, 0.08); color: var(--success); }
      .toast.error { border-color: rgba(239, 68, 68, 0.3); background: rgba(239, 68, 68, 0.08); color: var(--danger); }
      @keyframes slideIn { from { transform: translateX(400px); opacity: 0; } to { transform: translateX(0); opacity: 1; } }
      /* ============================================== INTERNAL OBSERVATIONS ============================================== */
      .internal-observations-section { margin-top: 32px; padding: 20px; background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); }
      .observations-title { font-size: 1.125rem; font-weight: 700; color: var(--text-primary); margin-bottom: 16px; display: flex; align-items: center; gap: 8px; }
      .observations-container { display: grid; grid-template-columns: 1fr; gap: 16px; }
      .agent-observation { padding: 12px; background: var(--surface-2); border: 1px solid var(--border); border-radius: var(--radius); display: grid; grid-template-columns: 200px 1fr auto; gap: 12px; align-items: stretch; }
      .agent-observation-select { display: flex; flex-direction: column; }
      .agent-observation-select label { font-size: 0.75rem; font-weight: 600; color: var(--text-secondary); margin-bottom: 6px; text-transform: uppercase; }
      .agent-observation-select select { flex: 1; padding: 8px 12px; background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); color: var(--text-primary); font-size: 0.95rem; }
      .agent-observation-textarea { display: flex; flex-direction: column; }
      .agent-observation-textarea label { font-size: 0.75rem; font-weight: 600; color: var(--text-secondary); margin-bottom: 6px; text-transform: uppercase; }
      .agent-observation-textarea textarea { flex: 1; padding: 8px 12px; background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); color: var(--text-primary); font-size: 0.95rem; font-family: inherit; resize: none; }
      .agent-observation-actions { display: flex; gap: 8px; align-items: flex-end; }
      .btn-add-observation { margin-top: 16px; padding: 10px 16px; background: var(--primary); border: 1px solid var(--primary); color: white; font-weight: 600; border-radius: var(--radius); cursor: pointer; }
      .btn-add-observation:hover { background: var(--primary-strong); border-color: var(--primary-strong); }
      /* ============================================== WEEKEND SCHEDULE ============================================== */
      .weekend-schedule-section { margin-top: 32px; padding: 20px; background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); }
      .schedule-title { font-size: 1.125rem; font-weight: 700; color: var(--text-primary); margin-bottom: 20px; }
      .schedule-day-title { font-size: 1rem; font-weight: 700; color: var(--text-primary); margin: 20px 0 12px 0; display: flex; align-items: center; gap: 8px; }
      .schedule-day-title::before { content: "📅"; font-size: 1.25rem; }
      .schedule-table { width: 100%; border-collapse: collapse; margin-bottom: 24px; background: var(--surface-2); border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden; }
      .schedule-table thead { background: var(--primary); color: white; }
      .schedule-table th { padding: 12px; text-align: center; font-weight: 600; font-size: 0.9rem; border-right: 1px solid var(--border); }
      .schedule-table td { padding: 12px; border: 1px solid var(--border); text-align: center; font-size: 0.95rem; }
      .schedule-table tbody tr:nth-child(odd) { background: var(--surface-2); }
      .schedule-time { font-weight: 600; color: var(--text-primary); min-width: 80px; background: rgba(37, 99, 235, 0.1); }
      .schedule-agent-select { padding: 6px; background: var(--surface); border: 1px solid var(--border); border-radius: 4px; color: var(--text-primary); font-size: 0.9rem; min-width: 140px; }
      .schedule-label { font-size: 0.8rem; color: var(--text-secondary); font-weight: 600; margin-bottom: 4px; display: block; }
      /* ============================================== OFF / VACATION SECTION ============================================== */
      .off-schedule-section { margin-top: 32px; padding: 20px; background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); }
      .off-schedule-title { font-size: 1.125rem; font-weight: 700; color: var(--text-primary); margin-bottom: 16px; display: flex; align-items: center; gap: 8px; }
      .off-schedule-grid { display: flex; flex-direction: column; gap: 8px; }
      .off-agent-card { padding: 10px 12px; background: var(--surface-2); border: 1px solid var(--border); border-radius: var(--radius); display: grid; grid-template-columns: 200px 1fr; gap: 12px; align-items: center; }
      .off-agent-name { font-weight: 600; color: var(--text-primary); font-size: 0.95rem; word-break: break-word; }
      .off-agent-status { display: flex; gap: 6px; flex-wrap: nowrap; justify-content: flex-start; }
      .off-status-btn { flex: 0 1 auto; min-width: auto; padding: 6px 12px; font-size: 0.8rem; font-weight: 600; border: 1px solid var(--border); border-radius: 4px; background: var(--surface); color: var(--text-primary); cursor: pointer; transition: all 0.2s; white-space: nowrap; }
      .off-status-btn:hover { border-color: var(--primary); background: rgba(37, 99, 235, 0.08); }
      .off-status-btn.active { background: var(--primary); border-color: var(--primary); color: white; }
      .off-status-btn.folga.active { background: var(--warning); border-color: var(--warning); }
      .off-status-btn.vacation.active { background: var(--danger); border-color: var(--danger); }
      .off-empty-state { grid-column: 1 / -1; padding: 32px; text-align: center; color: var(--text-secondary); font-size: 0.95rem; }
      /* ============================================== MONTH WEEKENDS SCHEDULES ============================================== */
      .month-weekends-section { margin-top: 32px; padding: 20px; background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); }
      .month-weekends-title { font-size: 1.25rem; font-weight: 700; color: var(--text-primary); margin-bottom: 20px; display: flex; align-items: center; gap: 8px; }
      .month-weekends-header { display: flex; gap: 12px; margin-bottom: 20px; flex-wrap: wrap; }
      .btn-generate-schedules { padding: 10px 16px; background: var(--primary); border: 1px solid var(--primary); color: white; font-weight: 600; border-radius: var(--radius); cursor: pointer; transition: all 0.2s; }
      .btn-generate-schedules:hover { background: var(--primary-strong); border-color: var(--primary-strong); }
      .month-weekends-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(500px, 1fr)); gap: 20px; margin-bottom: 20px; }
      @media (max-width: 1200px) { .month-weekends-grid { grid-template-columns: 1fr; } }
      .weekend-panel { background: var(--surface-2); border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden; }
      .weekend-panel-header { background: linear-gradient(135deg, var(--primary), var(--primary-strong)); color: white; padding: 14px 16px; font-weight: 700; font-size: 1rem; display: flex; align-items: center; gap: 8px; }
      .weekend-panel-content { padding: 16px; max-height: 600px; overflow-y: auto; }
      .weekend-day-section { margin-bottom: 16px; }
      .weekend-day-label { font-weight: 700; color: var(--text-primary); font-size: 0.95rem; margin-bottom: 10px; padding-bottom: 8px; border-bottom: 1px solid var(--border); }
      .weekend-shift-row { display: flex; gap: 10px; margin-bottom: 10px; align-items: center; font-size: 0.9rem; }
      .weekend-shift-label { min-width: 70px; color: var(--text-secondary); font-size: 0.85rem; font-weight: 500; }
      .weekend-agent-select { flex: 1; padding: 6px 8px; background: var(--surface); border: 1px solid var(--border); border-radius: 4px; color: var(--text-primary); font-size: 0.9rem; cursor: pointer; }
      .month-schedule-day-section { margin-bottom: 16px; }
      .month-schedule-day-title { font-size: 0.95rem; font-weight: 700; color: var(--text-primary); margin: 0 0 12px 0; display: flex; align-items: center; gap: 8px; }
      .month-schedule-day-title::before { content: "📅"; font-size: 1rem; }
      .month-schedule-day-section .schedule-table { width: 100%; border-collapse: collapse; background: var(--surface-2); border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden; margin: 0; }
      .month-schedule-day-section .schedule-table thead { background: var(--primary); color: white; }
      .month-schedule-day-section .schedule-table th { padding: 10px 8px; text-align: center; font-weight: 600; font-size: 0.85rem; border-right: 1px solid var(--border); }
      .month-schedule-day-section .schedule-table td { padding: 10px 8px; border: 1px solid var(--border); text-align: center; font-size: 0.9rem; }
      .month-schedule-day-section .schedule-table .schedule-time { font-weight: 600; color: var(--text-primary); min-width: 70px; background: rgba(37, 99, 235, 0.1); }
      .month-schedule-agent-select { padding: 6px 8px; background: var(--surface); border: 1px solid var(--border); border-radius: 4px; color: var(--text-primary); font-size: 0.9rem; cursor: pointer; min-width: 120px; width: 100%; }
      .month-off-schedule { margin-top: 20px; padding-top: 20px; border-top: 2px solid var(--border); }
      .month-off-schedule-title { font-size: 1rem; font-weight: 700; color: var(--text-primary); margin-bottom: 16px; display: flex; align-items: center; gap: 8px; }
      .month-off-schedule-grid { display: flex; flex-direction: column; gap: 8px; }
      .theme-toggle-btn { padding: 8px 12px; border-radius: var(--radius); border: 1px solid var(--border); }
    </style>
  </head>
  <body>
    </body>
</html>

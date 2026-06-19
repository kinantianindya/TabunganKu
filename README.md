<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>💜 Aplikasi Tabungan Sederhana</title>
    <style>
        :root {
            --primary: #7c3aed;
            --primary-dark: #5b21b6;
            --primary-light: #a78bfa;
            --primary-bg: #f5f0ff;
            --accent: #c084fc;
            --white: #ffffff;
            --gray-50: #fafafa;
            --gray-100: #f3f3f3;
            --gray-200: #e5e5e5;
            --gray-300: #d4d4d4;
            --gray-400: #a3a3a3;
            --gray-500: #737373;
            --gray-600: #525252;
            --gray-700: #404040;
            --gray-800: #262626;
            --gray-900: #171717;
            --green: #10b981;
            --green-bg: #ecfdf5;
            --red: #ef4444;
            --red-bg: #fef2f2;
            --radius-sm: 8px;
            --radius: 12px;
            --radius-lg: 16px;
            --radius-xl: 20px;
            --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
            --shadow: 0 1px 3px rgba(0, 0, 0, 0.1), 0 1px 2px rgba(0, 0, 0, 0.06);
            --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.07), 0 2px 4px rgba(0, 0, 0, 0.06);
            --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1), 0 4px 6px rgba(0, 0, 0, 0.05);
            --shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.1), 0 8px 10px rgba(0, 0, 0, 0.04);
            --transition: 0.2s cubic-bezier(0.4, 0, 0.2, 1);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', 'Inter', system-ui, -apple-system, sans-serif;
            background: linear-gradient(135deg, #ede9fe 0%, #f5f0ff 30%, #faf8ff 60%, #f3e8ff 100%);
            background-attachment: fixed;
            min-height: 100vh;
            color: var(--gray-800);
            line-height: 1.6;
            -webkit-font-smoothing: antialiased;
        }

        /* Decorative background blobs */
        body::before {
            content: '';
            position: fixed;
            top: -180px;
            right: -120px;
            width: 500px;
            height: 500px;
            background: radial-gradient(circle, rgba(167, 139, 250, 0.25) 0%, transparent 70%);
            border-radius: 50%;
            z-index: 0;
            pointer-events: none;
        }
        body::after {
            content: '';
            position: fixed;
            bottom: -150px;
            left: -100px;
            width: 450px;
            height: 450px;
            background: radial-gradient(circle, rgba(192, 132, 252, 0.2) 0%, transparent 70%);
            border-radius: 50%;
            z-index: 0;
            pointer-events: none;
        }

        .container {
            max-width: 650px;
            margin: 0 auto;
            padding: 20px 16px 40px;
            position: relative;
            z-index: 1;
        }

        /* Header */
        .header {
            text-align: center;
            padding: 28px 20px 16px;
        }
        .header .icon {
            font-size: 48px;
            display: block;
            margin-bottom: 4px;
            animation: float 3s ease-in-out infinite;
        }
        @keyframes float {
            0%,
            100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-10px);
            }
        }
        .header h1 {
            font-size: 1.75rem;
            font-weight: 700;
            color: var(--primary-dark);
            letter-spacing: -0.02em;
        }
        .header .subtitle {
            font-size: 0.9rem;
            color: var(--gray-500);
            margin-top: 2px;
        }

        /* Summary Cards */
        .summary-cards {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 12px;
            margin-bottom: 20px;
        }
        .summary-card {
            background: var(--white);
            border-radius: var(--radius-lg);
            padding: 16px 14px;
            text-align: center;
            box-shadow: var(--shadow-md);
            transition: var(--transition);
            border: 1.5px solid transparent;
            position: relative;
            overflow: hidden;
        }
        .summary-card:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow-xl);
        }
        .summary-card.income-card {
            border-color: #d1fae5;
            background: linear-gradient(180deg, #ffffff 0%, #f0fdf6 100%);
        }
        .summary-card.expense-card {
            border-color: #fee2e2;
            background: linear-gradient(180deg, #ffffff 0%, #fff5f5 100%);
        }
        .summary-card.balance-card {
            border-color: #ede9fe;
            background: linear-gradient(180deg, #ffffff 0%, #faf8ff 100%);
        }
        .summary-card .card-label {
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.04em;
            color: var(--gray-500);
            margin-bottom: 6px;
        }
        .summary-card .card-amount {
            font-size: 1.35rem;
            font-weight: 700;
            letter-spacing: -0.02em;
        }
        .summary-card.income-card .card-amount {
            color: #059669;
        }
        .summary-card.expense-card .card-amount {
            color: #dc2626;
        }
        .summary-card.balance-card .card-amount {
            color: var(--primary-dark);
        }
        .summary-card.balance-card .card-amount.negative {
            color: #dc2626;
        }
        .card-icon {
            font-size: 1.6rem;
            display: block;
            margin-bottom: 2px;
        }

        /* Form Card */
        .card {
            background: var(--white);
            border-radius: var(--radius-xl);
            padding: 22px 20px;
            margin-bottom: 18px;
            box-shadow: var(--shadow-lg);
            border: 1.5px solid #ede9fe;
            transition: var(--transition);
        }
        .card h2 {
            font-size: 1.1rem;
            font-weight: 700;
            color: var(--primary-dark);
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
            letter-spacing: -0.01em;
        }
        .card h2 .emoji {
            font-size: 1.3rem;
        }

        /* Form */
        .form-row {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-bottom: 12px;
        }
        .form-group {
            flex: 1;
            min-width: 120px;
            display: flex;
            flex-direction: column;
            gap: 4px;
        }
        .form-group label {
            font-size: 0.78rem;
            font-weight: 600;
            color: var(--gray-600);
            letter-spacing: 0.02em;
        }
        .form-group input,
        .form-group select {
            padding: 10px 14px;
            border: 2px solid var(--gray-200);
            border-radius: var(--radius);
            font-size: 0.9rem;
            font-family: inherit;
            transition: var(--transition);
            background: var(--gray-50);
            color: var(--gray-800);
            width: 100%;
            outline: none;
        }
        .form-group input:focus,
        .form-group select:focus {
            border-color: var(--primary-light);
            box-shadow: 0 0 0 3px rgba(167, 139, 250, 0.15);
            background: var(--white);
        }
        .form-group input::placeholder {
            color: var(--gray-400);
        }
        .btn {
            padding: 11px 24px;
            border: none;
            border-radius: var(--radius);
            font-size: 0.9rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            font-family: inherit;
            letter-spacing: 0.01em;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            justify-content: center;
        }
        .btn-primary {
            background: var(--primary);
            color: white;
            box-shadow: var(--shadow-md);
        }
        .btn-primary:hover {
            background: var(--primary-dark);
            box-shadow: var(--shadow-lg);
            transform: translateY(-1px);
        }
        .btn-primary:active {
            transform: scale(0.97);
            box-shadow: var(--shadow-sm);
        }
        .btn-full {
            width: 100%;
            margin-top: 4px;
        }

        /* Transaction List */
        .transaction-list-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        .transaction-count {
            font-size: 0.8rem;
            color: var(--gray-500);
            font-weight: 500;
            background: var(--primary-bg);
            padding: 4px 12px;
            border-radius: 20px;
        }
        .filter-buttons {
            display: flex;
            gap: 6px;
            flex-wrap: wrap;
            margin-bottom: 12px;
        }
        .filter-btn {
            padding: 7px 14px;
            border-radius: 20px;
            border: 2px solid var(--gray-200);
            background: var(--white);
            cursor: pointer;
            font-size: 0.78rem;
            font-weight: 600;
            transition: var(--transition);
            color: var(--gray-600);
            font-family: inherit;
            white-space: nowrap;
        }
        .filter-btn:hover {
            border-color: var(--primary-light);
            color: var(--primary);
        }
        .filter-btn.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
            box-shadow: var(--shadow-md);
        }
        .transaction-list {
            list-style: none;
            display: flex;
            flex-direction: column;
            gap: 8px;
            max-height: 420px;
            overflow-y: auto;
            padding-right: 4px;
        }
        .transaction-list::-webkit-scrollbar {
            width: 5px;
        }
        .transaction-list::-webkit-scrollbar-track {
            background: transparent;
            border-radius: 10px;
        }
        .transaction-list::-webkit-scrollbar-thumb {
            background: var(--gray-300);
            border-radius: 10px;
        }
        .transaction-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 14px 16px;
            border-radius: var(--radius-lg);
            background: var(--white);
            border: 1.5px solid var(--gray-100);
            transition: var(--transition);
            box-shadow: var(--shadow-sm);
            position: relative;
        }
        .transaction-item:hover {
            border-color: #e9d5ff;
            box-shadow: var(--shadow-md);
            transform: translateX(2px);
        }
        .transaction-item.income {
            border-left: 4px solid var(--green);
        }
        .transaction-item.expense {
            border-left: 4px solid var(--red);
        }
        .transaction-icon {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            flex-shrink: 0;
            font-weight: 700;
        }
        .transaction-item.income .transaction-icon {
            background: #d1fae5;
            color: #059669;
        }
        .transaction-item.expense .transaction-icon {
            background: #fee2e2;
            color: #dc2626;
        }
        .transaction-info {
            flex: 1;
            min-width: 0;
        }
        .transaction-info .desc {
            font-weight: 600;
            color: var(--gray-800);
            font-size: 0.9rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .transaction-info .meta {
            font-size: 0.73rem;
            color: var(--gray-500);
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }
        .transaction-info .meta .category-badge {
            background: var(--primary-bg);
            color: var(--primary-dark);
            padding: 2px 8px;
            border-radius: 10px;
            font-weight: 500;
            font-size: 0.7rem;
        }
        .transaction-amount {
            font-weight: 700;
            font-size: 1rem;
            letter-spacing: -0.02em;
            flex-shrink: 0;
            text-align: right;
        }
        .transaction-item.income .transaction-amount {
            color: #059669;
        }
        .transaction-item.expense .transaction-amount {
            color: #dc2626;
        }
        .delete-btn {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 1.1rem;
            padding: 6px 8px;
            border-radius: 50%;
            transition: var(--transition);
            color: var(--gray-400);
            flex-shrink: 0;
            line-height: 1;
        }
        .delete-btn:hover {
            background: #fef2f2;
            color: #ef4444;
            transform: scale(1.15);
        }
        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: var(--gray-400);
        }
        .empty-state .big-emoji {
            font-size: 3.5rem;
            display: block;
            margin-bottom: 8px;
        }
        .empty-state p {
            font-size: 0.9rem;
            font-weight: 500;
        }

        /* Toast */
        .toast {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%) translateY(120px);
            background: var(--gray-900);
            color: white;
            padding: 12px 24px;
            border-radius: 30px;
            font-weight: 600;
            font-size: 0.85rem;
            z-index: 100;
            opacity: 0;
            transition: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
            pointer-events: none;
            box-shadow: var(--shadow-xl);
            letter-spacing: 0.01em;
        }
        .toast.show {
            opacity: 1;
            transform: translateX(-50%) translateY(0);
        }
        .toast.success {
            background: #059669;
        }
        .toast.error {
            background: #dc2626;
        }

        /* Responsive */
        @media (max-width: 500px) {
            .summary-cards {
                grid-template-columns: 1fr 1fr;
                gap: 8px;
            }
            .summary-card.balance-card {
                grid-column: 1 / -1;
            }
            .form-row {
                flex-direction: column;
                gap: 8px;
            }
            .header h1 {
                font-size: 1.4rem;
            }
            .card {
                padding: 16px 14px;
            }
            .transaction-item {
                padding: 12px 12px;
                gap: 8px;
            }
            .transaction-amount {
                font-size: 0.9rem;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- Header -->
        <div class="header">
            <span class="icon">🐷</span>
            <h1>TabunganKu</h1>
            <p class="subtitle">Catat semua uang masuk & keluar dengan mudah 💜</p>
        </div>

        <!-- Summary Cards -->
        <div class="summary-cards">
            <div class="summary-card income-card">
                <span class="card-icon">📥</span>
                <div class="card-label">Total Masuk</div>
                <div class="card-amount" id="totalIncome">Rp0</div>
            </div>
            <div class="summary-card expense-card">
                <span class="card-icon">📤</span>
                <div class="card-label">Total Keluar</div>
                <div class="card-amount" id="totalExpense">Rp0</div>
            </div>
            <div class="summary-card balance-card">
                <span class="card-icon">💰</span>
                <div class="card-label">Saldo</div>
                <div class="card-amount" id="totalBalance">Rp0</div>
            </div>
        </div>

        <!-- Form Tambah Transaksi -->
        <div class="card">
            <h2><span class="emoji">✍️</span> Tambah Transaksi</h2>
            <form id="transactionForm">
                <div class="form-row">
                    <div class="form-group">
                        <label>Jenis Transaksi</label>
                        <select id="type" required>
                            <option value="income">📥 Pemasukan</option>
                            <option value="expense">📤 Pengeluaran</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Kategori Uang</label>
                        <select id="category" required>
                            <option value="Tunai">💵 Tunai</option>
                            <option value="Digital">📱 Digital (QRIS/Transfer)</option>
                            <option value="Bank">🏦 Rekening Bank</option>
                            <option value="E-Wallet">🪪 E-Wallet</option>
                            <option value="Lainnya">📦 Lainnya</option>
                        </select>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Deskripsi</label>
                        <input type="text" id="description" placeholder="Contoh: Gaji bulanan, beli kopi..." required maxlength="60">
                    </div>
                    <div class="form-group" style="max-width: 180px;">
                        <label>Jumlah (Rp)</label>
                        <input type="number" id="amount" placeholder="0" required min="1" step="1">
                    </div>
                </div>
                <button type="submit" class="btn btn-primary btn-full">
                    ➕ Tambah Transaksi
                </button>
            </form>
        </div>

        <!-- Daftar Transaksi -->
        <div class="card">
            <div class="transaction-list-header">
                <h2><span class="emoji">📋</span> Riwayat Transaksi</h2>
                <span class="transaction-count" id="transactionCount">0 catatan</span>
            </div>
            <div class="filter-buttons">
                <button class="filter-btn active" data-filter="all">📋 Semua</button>
                <button class="filter-btn" data-filter="income">📥 Masuk</button>
                <button class="filter-btn" data-filter="expense">📤 Keluar</button>
            </div>
            <ul class="transaction-list" id="transactionList">
                <li class="empty-state">
                    <span class="big-emoji">📭</span>
                    <p>Belum ada transaksi</p>
                    <p style="font-size:0.75rem;color:#c4b5fd;">Yuk, mulai catat uangmu!</p>
                </li>
            </ul>
        </div>
    </div>

    <!-- Toast Notification -->
    <div class="toast" id="toast"></div>

    <script>
        // ========== DATA STORAGE ==========
        const STORAGE_KEY = 'tabunganku_transactions';

        function getTransactions() {
            const raw = localStorage.getItem(STORAGE_KEY);
            if (!raw) return [];
            try {
                return JSON.parse(raw);
            } catch (e) {
                return [];
            }
        }

        function saveTransactions(transactions) {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(transactions));
        }

        // ========== FORMAT RUPIAH ==========
        function formatRupiah(amount) {
            if (amount === 0) return 'Rp0';
            const sign = amount < 0 ? '-' : '';
            const abs = Math.abs(amount);
            const formatted = abs.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.');
            return sign + 'Rp' + formatted;
        }

        // ========== TOAST ==========
        function showToast(message, type = '') {
            const toast = document.getElementById('toast');
            toast.textContent = message;
            toast.className = 'toast ' + type + ' show';
            clearTimeout(toast._timeout);
            toast._timeout = setTimeout(() => {
                toast.classList.remove('show');
            }, 2200);
        }

        // ========== RENDER ==========
        let currentFilter = 'all';

        function renderAll() {
            const transactions = getTransactions();
            const filtered = currentFilter === 'all' ?
                transactions :
                transactions.filter(t => t.type === currentFilter);

            // Hitung total
            let totalIncome = 0;
            let totalExpense = 0;
            transactions.forEach(t => {
                if (t.type === 'income') totalIncome += t.amount;
                else totalExpense += t.amount;
            });
            const balance = totalIncome - totalExpense;

            // Update summary cards
            document.getElementById('totalIncome').textContent = formatRupiah(totalIncome);
            document.getElementById('totalExpense').textContent = formatRupiah(totalExpense);
            const balanceEl = document.getElementById('totalBalance');
            balanceEl.textContent = formatRupiah(balance);
            if (balance < 0) {
                balanceEl.classList.add('negative');
            } else {
                balanceEl.classList.remove('negative');
            }

            // Update transaction count
            document.getElementById('transactionCount').textContent =
                filtered.length + ' catatan';

            // Render list
            const listEl = document.getElementById('transactionList');
            if (filtered.length === 0) {
                listEl.innerHTML = `
                        <li class="empty-state">
                            <span class="big-emoji">📭</span>
                            <p>Belum ada transaksi</p>
                            <p style="font-size:0.75rem;color:#c4b5fd;">Yuk, mulai catat uangmu!</p>
                        </li>`;
                return;
            }

            // Sort by newest first (based on id/timestamp)
            const sorted = [...filtered].reverse();

            listEl.innerHTML = sorted.map((t, index) => {
                const isIncome = t.type === 'income';
                const icon = isIncome ? '↓' : '↑';
                const sign = isIncome ? '+' : '-';
                const dateStr = new Date(t.id).toLocaleDateString('id-ID', {
                    day: 'numeric',
                    month: 'short',
                    year: 'numeric',
                    hour: '2-digit',
                    minute: '2-digit'
                });
                return `
                        <li class="transaction-item ${t.type}" data-id="${t.id}">
                            <div class="transaction-icon">${icon}</div>
                            <div class="transaction-info">
                                <div class="desc">${escapeHTML(t.description)}</div>
                                <div class="meta">
                                    <span>${dateStr}</span>
                                    <span class="category-badge">${escapeHTML(t.category)}</span>
                                </div>
                            </div>
                            <div class="transaction-amount">${sign} ${formatRupiah(Math.abs(t.amount))}</div>
                            <button class="delete-btn" onclick="deleteTransaction(${t.id})" title="Hapus">🗑️</button>
                        </li>`;
            }).join('');
        }

        function escapeHTML(str) {
            const div = document.createElement('div');
            div.textContent = str;
            return div.innerHTML;
        }

        // ========== ADD TRANSACTION ==========
        document.getElementById('transactionForm').addEventListener('submit', function(e) {
            e.preventDefault();

            const type = document.getElementById('type').value;
            const category = document.getElementById('category').value;
            const description = document.getElementById('description').value.trim();
            const amountRaw = document.getElementById('amount').value;

            if (!description || !amountRaw || parseInt(amountRaw) < 1) {
                showToast('⚠️ Mohon isi semua data dengan benar!', 'error');
                return;
            }

            const amount = parseInt(amountRaw);
            const transaction = {
                id: Date.now(),
                type: type,
                category: category,
                description: description,
                amount: amount,
            };

            const transactions = getTransactions();
            transactions.push(transaction);
            saveTransactions(transactions);

            // Reset form
            document.getElementById('description').value = '';
            document.getElementById('amount').value = '';
            document.getElementById('description').focus();

            renderAll();
            showToast('✅ Transaksi berhasil dicatat!', 'success');
        });

        // ========== DELETE TRANSACTION ==========
        function deleteTransaction(id) {
            let transactions = getTransactions();
            const target = transactions.find(t => t.id === id);
            transactions = transactions.filter(t => t.id !== id);
            saveTransactions(transactions);
            renderAll();
            if (target) {
                showToast('🗑️ Transaksi dihapus!', 'error');
            }
        }

        // ========== FILTER BUTTONS ==========
        document.querySelectorAll('.filter-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove(
                    'active'));
                this.classList.add('active');
                currentFilter = this.dataset.filter;
                renderAll();
            });
        });

        // ========== INITIAL RENDER ==========
        renderAll();

        // ========== FOCUS DESCRIPTION ON LOAD ==========
        document.getElementById('description').focus();

        console.log('💜 Aplikasi TabunganKu siap digunakan!');
        console.log('   Catat semua pemasukan & pengeluaran');
        console.log('   Support: Tunai, Digital, Bank, E-Wallet, dll.');
        console.log('   Data tersimpan di localStorage browser Anda.');
    </script>
</body>
</html>

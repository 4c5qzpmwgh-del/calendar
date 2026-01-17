<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>預約行事曆 WebApp</title>
    
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" content="#FFFAF0">

    <script src="https://cdn.tailwindcss.com"></script>
    
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        /* 自定義字型與動畫 */
        @import url('https://fonts.googleapis.com/css2?family=Nunito:wght@400;700&family=Noto+Sans+TC:wght@400;700&display=swap');

        body {
            font-family: 'Nunito', 'Noto Sans TC', sans-serif;
            background-color: #FFF8E7; /* 奶油色背景 */
            overscroll-behavior-y: none; /* 防止手機下拉刷新 */
        }

        /* 隱藏滾動條但保留功能 */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }

        /* 3D 翻轉卡片核心 CSS */
        .perspective-1000 {
            perspective: 1000px;
        }
        .flip-card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.6s;
            transform-style: preserve-3d;
        }
        .flip-card.flipped .flip-card-inner {
            transform: rotateY(180deg);
        }
        .flip-card-front, .flip-card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            border-radius: 1rem;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: flex-start;
            padding: 1rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
        .flip-card-back {
            transform: rotateY(180deg);
            background-color: #ffffff;
            border: 2px solid #FCD34D;
        }

        /* 活潑的按鈕動畫 */
        .btn-bounce:active {
            transform: scale(0.95);
        }

        /* 選中日期的特效 */
        .selected-date {
            background-color: #F59E0B;
            color: white;
            border-radius: 50%;
            box-shadow: 0 0 10px rgba(245, 158, 11, 0.5);
        }
    </style>
</head>
<body class="h-screen w-screen overflow-hidden text-gray-700">

    <div id="app" class="h-full flex flex-col relative">

        <header class="pt-12 pb-4 px-6 bg-yellow-300 rounded-b-3xl shadow-lg z-10 flex justify-between items-center">
            <div>
                <h1 class="text-3xl font-bold text-yellow-900">{{ currentTime }}</h1>
                <p class="text-sm font-bold text-yellow-800 opacity-80">{{ currentDateString }}</p>
            </div>
            <button @click="openAddModal" class="bg-white text-yellow-500 w-10 h-10 rounded-full shadow-md flex items-center justify-center btn-bounce">
                <i class="fas fa-plus text-xl"></i>
            </button>
        </header>

        <main class="flex-1 overflow-y-auto no-scrollbar pb-24 px-4 pt-4">
            
            <div v-show="currentView === 'home'">
                <div class="bg-white rounded-2xl p-4 shadow-sm mb-6">
                    <div class="flex justify-between items-center mb-4">
                        <button @click="changeMonth(-1)" class="text-gray-400 hover:text-gray-600"><i class="fas fa-chevron-left"></i></button>
                        <h2 class="text-lg font-bold text-gray-700">{{ calendarTitle }}</h2>
                        <button @click="changeMonth(1)" class="text-gray-400 hover:text-gray-600"><i class="fas fa-chevron-right"></i></button>
                    </div>
                    <div class="grid grid-cols-7 gap-2 text-center text-sm">
                        <div v-for="day in ['日','一','二','三','四','五','六']" class="text-gray-400 text-xs">{{ day }}</div>
                        <div v-for="blank in blankDays" :key="'blank'+blank"></div>
                        <div v-for="date in daysInMonth" :key="date" 
                             @click="selectDate(date)"
                             class="h-8 w-8 flex items-center justify-center rounded-full cursor-pointer transition-colors relative"
                             :class="isSelected(date) ? 'selected-date' : 'hover:bg-gray-100'">
                            {{ date }}
                            <span v-if="hasEvent(date)" class="absolute bottom-0.5 w-1 h-1 bg-red-400 rounded-full"></span>
                        </div>
                    </div>
                </div>

                <div class="mb-2 flex justify-between items-end">
                    <h3 class="text-xl font-bold text-gray-800">今日行程</h3>
                    <span class="text-xs text-gray-500">點擊卡片查看詳情</span>
                </div>

                <div v-if="todaysEvents.length === 0" class="text-center py-10 opacity-50">
                    <i class="fas fa-coffee text-4xl mb-2 text-gray-300"></i>
                    <p>今天沒有安排行程，放鬆一下吧！</p>
                </div>

                <div class="space-y-4">
                    <div v-for="event in todaysEvents" :key="event.id" 
                         class="flip-card h-32 w-full perspective-1000 cursor-pointer"
                         :class="{ flipped: event.isFlipped }"
                         @click="toggleFlip(event)">
                        <div class="flip-card-inner">
                            <div class="flip-card-front bg-gradient-to-br from-blue-100 to-blue-50 border-l-4 border-blue-400">
                                <div class="flex justify-between w-full items-start">
                                    <span class="bg-blue-200 text-blue-800 text-xs px-2 py-1 rounded-full font-bold">
                                        {{ formatTime(event.time) }}
                                    </span>
                                    <i v-if="event.isReservation" class="fas fa-calendar-check text-blue-300"></i>
                                </div>
                                <h4 class="text-xl font-bold mt-2">{{ event.title }}</h4>
                                <p class="text-sm text-gray-500 line-clamp-1">{{ event.desc }}</p>
                            </div>
                            <div class="flip-card-back">
                                <div class="w-full h-full flex flex-col justify-between">
                                    <div>
                                        <h5 class="text-sm font-bold text-gray-400 mb-1">詳細內容</h5>
                                        <p v-if="event.isReservation" class="text-sm">
                                            <span class="font-bold text-gray-800">預約人：</span>{{ event.resName }}<br>
                                            <span class="font-bold text-gray-800">項目：</span>{{ event.resItem }}
                                        </p>
                                        <p v-else class="text-sm text-gray-600">{{ event.desc || '無詳細說明' }}</p>
                                    </div>
                                    <div class="flex justify-between items-center w-full mt-2">
                                        <button @click.stop="deleteEvent(event.id)" class="text-red-400 text-xs hover:text-red-600">
                                            <i class="fas fa-trash"></i> 刪除
                                        </button>
                                        <span class="text-xs text-gray-400">再點擊一次翻回</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="mt-8 mb-4">
                    <h3 class="text-xl font-bold text-gray-800 mb-2">今日花費</h3>
                    <div class="bg-white rounded-xl p-4 shadow-sm border border-gray-100">
                        <div v-for="exp in todaysExpenses" :key="exp.id" class="flex justify-between items-center py-2 border-b border-gray-50 last:border-0">
                            <span class="text-gray-600">{{ exp.title }}</span>
                            <span class="font-bold text-red-500">NT$ {{ exp.amount }}</span>
                        </div>
                        <div v-if="todaysExpenses.length === 0" class="text-center text-sm text-gray-400 py-2">本日尚無消費紀錄</div>
                        
                        <div class="mt-4 flex gap-2">
                            <input v-model="newExpenseTitle" type="text" placeholder="項目" class="w-1/2 bg-gray-50 rounded px-2 py-1 text-sm outline-none focus:ring-1 focus:ring-yellow-300">
                            <input v-model="newExpenseAmount" type="number" placeholder="$" class="w-1/4 bg-gray-50 rounded px-2 py-1 text-sm outline-none focus:ring-1 focus:ring-yellow-300">
                            <button @click="addExpense" class="w-1/4 bg-yellow-400 text-white rounded text-sm font-bold btn-bounce">記帳</button>
                        </div>
                    </div>
                </div>
            </div>

            <div v-show="currentView === 'stats'" class="animate-fade-in">
                <h2 class="text-2xl font-bold text-gray-800 mb-6">消費統計</h2>
                
                <div class="bg-gradient-to-r from-red-400 to-pink-500 rounded-2xl p-6 text-white shadow-lg mb-6">
                    <p class="text-sm opacity-80">本月總支出</p>
                    <h3 class="text-4xl font-bold mt-1">NT$ {{ monthlyTotal }}</h3>
                </div>

                <div class="bg-white rounded-2xl p-4 shadow-sm h-64 relative">
                    <canvas id="expenseChart"></canvas>
                </div>

                <div class="mt-6 text-center text-gray-400 text-sm">
                    <p>繼續保持記帳的好習慣！</p>
                </div>
            </div>

        </main>

        <nav class="fixed bottom-0 w-full bg-white border-t border-gray-100 pb-safe pt-2 px-6 flex justify-around items-center z-20 pb-4 rounded-t-3xl shadow-[0_-5px_20px_rgba(0,0,0,0.05)]">
            <button @click="switchView('home')" :class="currentView === 'home' ? 'text-yellow-500' : 'text-gray-300'" class="flex flex-col items-center btn-bounce">
                <i class="fas fa-calendar-alt text-2xl mb-1"></i>
                <span class="text-xs">日程</span>
            </button>
            <button @click="openAddModal" class="bg-yellow-400 text-white -mt-10 w-14 h-14 rounded-full shadow-lg flex items-center justify-center btn-bounce border-4 border-[#FFFAF0]">
                <i class="fas fa-plus text-2xl"></i>
            </button>
            <button @click="switchView('stats')" :class="currentView === 'stats' ? 'text-yellow-500' : 'text-gray-300'" class="flex flex-col items-center btn-bounce">
                <i class="fas fa-chart-pie text-2xl mb-1"></i>
                <span class="text-xs">統計</span>
            </button>
        </nav>

        <div v-if="showModal" class="fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center p-4">
            <div class="bg-white w-full max-w-sm rounded-2xl p-6 shadow-2xl animate-bounce-in">
                <h3 class="text-xl font-bold mb-4">新增行程</h3>
                
                <div class="space-y-3">
                    <div>
                        <label class="text-xs text-gray-400">行程</label>
                        <input v-model="newEvent.title" type="text" class="w-full border-b-2 border-gray-100 focus:border-yellow-400 outline-none py-1 text-lg">
                    </div>
                    <div>
                        <label class="text-xs text-gray-400">行程描述</label>
                        <textarea v-model="newEvent.desc" rows="2" class="w-full bg-gray-50 rounded p-2 text-sm outline-none mt-1"></textarea>
                    </div>
                    <div class="flex gap-2">
                        <div class="w-1/2">
                            <label class="text-xs text-gray-400">日期</label>
                            <input v-model="newEvent.date" type="date" class="w-full bg-gray-50 rounded p-2 text-sm">
                        </div>
                        <div class="w-1/2">
                            <label class="text-xs text-gray-400">時間</label>
                            <input v-model="newEvent.time" type="time" step="1" class="w-full bg-gray-50 rounded p-2 text-sm">
                        </div>
                    </div>

                    <div class="flex items-center gap-2 mt-2">
                        <input type="checkbox" id="isRes" v-model="newEvent.isReservation" class="w-4 h-4 text-yellow-400 rounded focus:ring-yellow-400">
                        <label for="isRes" class="text-sm font-bold text-gray-700">這是一個預約</label>
                    </div>

                    <div v-if="newEvent.isReservation" class="bg-yellow-50 p-3 rounded-lg space-y-2 border border-yellow-100">
                        <input v-model="newEvent.resName" type="text" placeholder="預約人姓名" class="w-full bg-white rounded px-2 py-1 text-sm">
                        <input v-model="newEvent.resItem" type="text" placeholder="預約項目 (如: 剪髮)" class="w-full bg-white rounded px-2 py-1 text-sm">
                    </div>
                </div>

                <div class="flex gap-2 mt-6">
                    <button @click="showModal = false" class="w-1/2 py-2 text-gray-400 font-bold rounded-lg bg-gray-100 hover:bg-gray-200">取消</button>
                    <button @click="saveEvent" class="w-1/2 py-2 text-white font-bold rounded-lg bg-yellow-400 hover:bg-yellow-500 shadow-md">儲存</button>
                </div>
            </div>
        </div>

    </div>

    <script>
        const { createApp, ref, computed, onMounted, watch, nextTick } = Vue;

        createApp({
            setup() {
                // --- 狀態變數 ---
                const currentView = ref('home');
                const showModal = ref(false);
                const currentTime = ref('');
                const currentDate = ref(new Date()); // 當前選擇查看的日期
                const today = new Date(); // 真實的今天

                // 資料存儲
                const events = ref([]);
                const expenses = ref([]);

                // 新增相關
                const newEvent = ref({
                    title: '', desc: '', date: '', time: '', 
                    isReservation: false, resName: '', resItem: ''
                });
                const newExpenseTitle = ref('');
                const newExpenseAmount = ref('');

                // Chart 實例
                let chartInstance = null;

                // --- 核心邏輯 ---

                // 1. 時鐘
                setInterval(() => {
                    const now = new Date();
                    currentTime.value = now.toLocaleTimeString('en-US', { hour12: false });
                }, 1000);

                const currentDateString = computed(() => {
                    return currentDate.value.toLocaleDateString('zh-TW', { year: 'numeric', month: 'long', day: 'numeric', weekday: 'long' });
                });

                // 2. 月曆邏輯
                const calendarTitle = computed(() => {
                    return currentDate.value.toLocaleDateString('zh-TW', { year: 'numeric', month: 'long' });
                });

                const daysInMonth = computed(() => {
                    const year = currentDate.value.getFullYear();
                    const month = currentDate.value.getMonth();
                    return new Date(year, month + 1, 0).getDate();
                });

                const blankDays = computed(() => {
                    const year = currentDate.value.getFullYear();
                    const month = currentDate.value.getMonth();
                    return new Date(year, month, 1).getDay();
                });

                function changeMonth(delta) {
                    const newDate = new Date(currentDate.value);
                    newDate.setMonth(newDate.getMonth() + delta);
                    currentDate.value = newDate;
                }

                function selectDate(day) {
                    const newDate = new Date(currentDate.value);
                    newDate.setDate(day);
                    currentDate.value = newDate;
                    
                    // 預設表單日期
                    newEvent.value.date = formatDateForInput(newDate);
                }

                function isSelected(day) {
                    return day === currentDate.value.getDate();
                }

                function formatDateForInput(date) {
                    const offset = date.getTimezoneOffset();
                    date = new Date(date.getTime() - (offset*60*1000));
                    return date.toISOString().split('T')[0];
                }

                // 3. 資料處理 (Event & Expense)
                const todaysEvents = computed(() => {
                    const targetDate = formatDateForInput(currentDate.value);
                    return events.value.filter(e => e.date === targetDate)
                                     .sort((a, b) => a.time.localeCompare(b.time));
                });

                const todaysExpenses = computed(() => {
                    const targetDate = formatDateForInput(currentDate.value);
                    return expenses.value.filter(e => e.date === targetDate);
                });

                const monthlyTotal = computed(() => {
                    // 簡單計算本月所有支出
                    const year = currentDate.value.getFullYear();
                    const month = currentDate.value.getMonth();
                    return expenses.value.filter(e => {
                        const d = new Date(e.date);
                        return d.getFullYear() === year && d.getMonth() === month;
                    }).reduce((sum, item) => sum + Number(item.amount), 0);
                });

                function hasEvent(day) {
                    const year = currentDate.value.getFullYear();
                    const month = currentDate.value.getMonth();
                    const checkDate = new Date(year, month, day);
                    const dateStr = formatDateForInput(checkDate);
                    return events.value.some(e => e.date === dateStr);
                }

                // 4. 互動操作
                function openAddModal() {
                    newEvent.value = {
                        title: '', desc: '', 
                        date: formatDateForInput(currentDate.value), 
                        time: '12:00', 
                        isReservation: false, resName: '', resItem: ''
                    };
                    showModal.value = true;
                }

                function saveEvent() {
                    if(!newEvent.value.title) return alert('請輸入標題');
                    
                    events.value.push({
                        id: Date.now(),
                        ...newEvent.value,
                        isFlipped: false
                    });
                    
                    saveData();
                    showModal.value = false;
                }

                function deleteEvent(id) {
                    if(confirm('確定刪除此行程？')) {
                        events.value = events.value.filter(e => e.id !== id);
                        saveData();
                    }
                }

                function toggleFlip(event) {
                    event.isFlipped = !event.isFlipped;
                }

                function addExpense() {
                    if(!newExpenseTitle.value || !newExpenseAmount.value) return;
                    expenses.value.push({
                        id: Date.now(),
                        title: newExpenseTitle.value,
                        amount: newExpenseAmount.value,
                        date: formatDateForInput(currentDate.value)
                    });
                    newExpenseTitle.value = '';
                    newExpenseAmount.value = '';
                    saveData();
                    
                    // 如果在統計頁面，刷新圖表
                    if(currentView.value === 'stats') updateChart();
                }

                function formatTime(timeStr) {
                    return timeStr.slice(0, 5); // 只顯示 HH:MM
                }

                // 5. 儲存與讀取
                function saveData() {
                    localStorage.setItem('myApp_events', JSON.stringify(events.value));
                    localStorage.setItem('myApp_expenses', JSON.stringify(expenses.value));
                }

                function loadData() {
                    const e = localStorage.getItem('myApp_events');
                    const ex = localStorage.getItem('myApp_expenses');
                    if(e) events.value = JSON.parse(e);
                    if(ex) expenses.value = JSON.parse(ex);
                    
                    // 恢復翻頁狀態為 false
                    events.value.forEach(ev => ev.isFlipped = false);
                }

                // 6. 圖表
                function switchView(view) {
                    currentView.value = view;
                    if(view === 'stats') {
                        nextTick(() => {
                            initChart();
                        });
                    }
                }

                function initChart() {
                    const ctx = document.getElementById('expenseChart');
                    if(!ctx) return;
                    
                    // 準備數據：最近7天
                    const labels = [];
                    const data = [];
                    for(let i=6; i>=0; i--) {
                        const d = new Date();
                        d.setDate(d.getDate() - i);
                        const dStr = formatDateForInput(d);
                        labels.push(d.getDate() + '日');
                        
                        const daySum = expenses.value
                            .filter(e => e.date === dStr)
                            .reduce((sum, item) => sum + Number(item.amount), 0);
                        data.push(daySum);
                    }

                    if(chartInstance) chartInstance.destroy();

                    chartInstance = new Chart(ctx, {
                        type: 'line',
                        data: {
                            labels: labels,
                            datasets: [{
                                label: '近七日花費',
                                data: data,
                                borderColor: '#FBBF24',
                                backgroundColor: 'rgba(251, 191, 36, 0.2)',
                                tension: 0.4,
                                fill: true
                            }]
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            plugins: {
                                legend: { display: false }
                            },
                            scales: {
                                y: { beginAtZero: true, grid: { display: false } },
                                x: { grid: { display: false } }
                            }
                        }
                    });
                }

                function updateChart() {
                    if(currentView.value === 'stats') initChart();
                }

                // 初始化
                onMounted(() => {
                    loadData();
                    currentTime.value = new Date().toLocaleTimeString('en-US', { hour12: false });
                    
                    // 預設一筆測試資料
                    if(events.value.length === 0) {
                        events.value.push({
                            id: 1,
                            title: '歡迎使用！',
                            desc: '試著點擊這張卡片翻面看看',
                            date: formatDateForInput(new Date()),
                            time: '09:00:00',
                            isReservation: true,
                            resName: '開發者',
                            resItem: '初次體驗',
                            isFlipped: false
                        });
                    }
                });

                return {
                    currentView, showModal, currentTime, currentDateString, calendarTitle,
                    daysInMonth, blankDays, changeMonth, selectDate, isSelected, hasEvent,
                    todaysEvents, todaysExpenses, monthlyTotal,
                    newEvent, newExpenseTitle, newExpenseAmount,
                    openAddModal, saveEvent, deleteEvent, toggleFlip, addExpense, formatTime, switchView
                };
            }
        }).mount('#app');
    </script>
</body>
</html>

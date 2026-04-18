[nourish-meal-planner](https://github.com/user-attachments/files/26860495/nourish-meal-planner.1.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nourish — Meal Planner & Calorie Tracker</title>
<meta name="description" content="Plan meals, track calories, protein, carbs and discover recipes in any language.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:wght@400;500;700&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --green:#2d6a4f;--green-light:#d8f3dc;--green-mid:#52b788;--green-dark:#1b4332;
  --blue:#1565c0;--blue-light:#e3f2fd;
  --amber:#e65100;--amber-light:#fff3e0;
  --red:#c62828;--red-light:#fdecea;
  --bg:#f7f9f6;--card:#fff;--border:#e0e7e3;--border2:#c8d5ce;
  --text:#1a2e24;--muted:#6b8278;--muted2:#94a89f;
  --radius:14px;--shadow:0 2px 12px rgba(45,106,79,.08);
}
@media(prefers-color-scheme:dark){
  :root{
    --bg:#0f1a14;--card:#1a2820;--border:#273d30;--border2:#3a5244;
    --text:#e8f5ee;--muted:#7aab8e;--muted2:#4d7a62;
    --green-light:#1b3a27;--blue-light:#0d2038;--amber-light:#2a1800;--red-light:#2a0a0a;
    --shadow:0 2px 12px rgba(0,0,0,.3);
  }
}
html{font-size:16px}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;line-height:1.5}

/* NAV */
nav{background:var(--card);border-bottom:1px solid var(--border);padding:0 1.5rem;display:flex;align-items:center;justify-content:space-between;height:58px;position:sticky;top:0;z-index:50;box-shadow:var(--shadow)}
.brand{font-family:'Fraunces',serif;font-size:22px;font-weight:700;color:var(--text);text-decoration:none}
.brand span{color:var(--green-mid)}
.nav-tabs{display:flex;gap:2px}
.nav-tab{background:none;border:none;padding:8px 16px;border-radius:8px;font-size:14px;cursor:pointer;color:var(--muted);font-family:'DM Sans',sans-serif;font-weight:400;transition:all .15s}
.nav-tab.active,.nav-tab:hover{background:var(--green-light);color:var(--green)}
.nav-tab.active{font-weight:500}
.lang-select{background:var(--bg);border:1px solid var(--border);border-radius:8px;padding:6px 10px;font-size:13px;color:var(--text);font-family:'DM Sans',sans-serif;cursor:pointer;outline:none}

/* LAYOUT */
.container{max-width:820px;margin:0 auto;padding:1.5rem 1rem}
.view{display:none}
.view.active{display:block}

/* SUMMARY CARDS */
.summary-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-bottom:1.5rem}
.stat-card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);padding:14px 16px;box-shadow:var(--shadow)}
.stat-label{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.06em;margin-bottom:6px;font-weight:500}
.stat-val{font-size:28px;font-weight:500;font-family:'Fraunces',serif;color:var(--text)}
.stat-unit{font-size:14px;color:var(--muted);font-family:'DM Sans',sans-serif}
.stat-sub{font-size:12px;color:var(--muted);margin-top:3px}
.progress-bar{height:5px;background:var(--border);border-radius:3px;margin-top:10px;overflow:hidden}
.progress-fill{height:100%;border-radius:3px;transition:width .5s ease}
.cal-fill{background:var(--green-mid)}
.prot-fill{background:#42a5f5}
.carb-fill{background:#ffa726}
.over{background:var(--red)}

/* DATE NAV */
.date-row{display:flex;align-items:center;gap:10px;margin-bottom:1.25rem}
.date-btn{background:var(--card);border:1px solid var(--border);border-radius:8px;width:34px;height:34px;display:flex;align-items:center;justify-content:center;cursor:pointer;font-size:16px;color:var(--muted);transition:all .15s}
.date-btn:hover{border-color:var(--green-mid);color:var(--green)}
.date-label{font-family:'Fraunces',serif;font-size:17px;font-weight:500;flex:1}

/* MEALS */
.meals-wrap{display:flex;flex-direction:column;gap:10px}
.meal-card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);box-shadow:var(--shadow);overflow:hidden}
.meal-header{display:flex;align-items:center;justify-content:space-between;padding:12px 16px;cursor:pointer;user-select:none;transition:background .15s}
.meal-header:hover{background:var(--bg)}
.meal-left{display:flex;align-items:center;gap:10px}
.meal-icon{width:34px;height:34px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:17px;flex-shrink:0}
.meal-name{font-size:15px;font-weight:500}
.meal-stats{font-size:12px;color:var(--muted);margin-top:1px}
.meal-right{display:flex;align-items:center;gap:10px}
.meal-kcal{font-family:'Fraunces',serif;font-size:16px;font-weight:500}
.chevron{color:var(--muted);font-size:11px;transition:transform .2s}
.chevron.open{transform:rotate(180deg)}
.meal-body{display:none;border-top:1px solid var(--border)}
.meal-body.open{display:block}
.food-list{padding:10px 16px;display:flex;flex-direction:column;gap:6px}
.food-row{display:flex;align-items:center;gap:8px;font-size:13px;padding:4px 0;border-bottom:1px solid var(--border)}
.food-row:last-child{border-bottom:none}
.food-name{flex:1;color:var(--text)}
.food-num{min-width:48px;text-align:right;color:var(--muted)}
.food-prot{min-width:44px;text-align:right;color:#42a5f5;font-size:12px}
.food-del{background:none;border:none;cursor:pointer;color:var(--muted2);padding:2px 5px;border-radius:5px;font-size:15px;line-height:1;transition:all .15s}
.food-del:hover{color:var(--red);background:var(--red-light)}
.add-section{padding:10px 16px 14px;background:var(--bg)}
.add-grid{display:grid;grid-template-columns:2fr 1fr 1fr 1fr auto;gap:6px;margin-bottom:8px}
.add-grid input{font-size:13px;padding:7px 10px;border:1px solid var(--border);border-radius:8px;background:var(--card);color:var(--text);font-family:'DM Sans',sans-serif;width:100%;outline:none;transition:border .15s}
.add-grid input:focus{border-color:var(--green-mid)}
.add-grid input::placeholder{color:var(--muted2)}
.add-btn{background:var(--green);color:#fff;border:none;border-radius:8px;padding:7px 14px;font-size:13px;cursor:pointer;font-family:'DM Sans',sans-serif;font-weight:500;white-space:nowrap;transition:opacity .15s}
.add-btn:hover{opacity:.88}
.ai-meal-btn{display:flex;align-items:center;gap:6px;background:none;border:1px solid var(--border);border-radius:8px;padding:7px 12px;font-size:13px;cursor:pointer;color:var(--muted);font-family:'DM Sans',sans-serif;width:100%;transition:all .15s}
.ai-meal-btn:hover{border-color:var(--green-mid);color:var(--green);background:var(--green-light)}
.ai-spark{font-size:14px}
.ai-box{background:var(--green-light);border:1px solid var(--green-mid);border-radius:10px;padding:10px 12px;font-size:13px;color:var(--green-dark);margin-top:8px;display:none;line-height:1.6}
.ai-box.show{display:block}
@media(prefers-color-scheme:dark){.ai-box{color:var(--green-mid)}}

/* RECIPES */
.section-title{font-family:'Fraunces',serif;font-size:20px;font-weight:700;margin-bottom:14px;color:var(--text)}
.recipe-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(175px,1fr));gap:12px}
.recipe-card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);padding:16px;cursor:pointer;transition:all .18s;box-shadow:var(--shadow)}
.recipe-card:hover{border-color:var(--green-mid);transform:translateY(-2px);box-shadow:0 6px 20px rgba(45,106,79,.12)}
.recipe-emoji{font-size:28px;margin-bottom:8px}
.recipe-name{font-size:14px;font-weight:500;margin-bottom:4px;color:var(--text)}
.recipe-macro{font-size:12px;color:var(--muted)}
.recipe-tag{display:inline-block;font-size:10px;padding:2px 8px;border-radius:20px;background:var(--green-light);color:var(--green);margin-top:6px;font-weight:500}

/* MODAL */
.modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:200;align-items:center;justify-content:center;padding:1rem}
.modal-bg.open{display:flex}
.modal{background:var(--card);border-radius:18px;padding:24px;max-width:440px;width:100%;border:1px solid var(--border);max-height:85vh;overflow-y:auto;box-shadow:0 20px 60px rgba(0,0,0,.2)}
.modal-top{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:4px}
.modal-title{font-family:'Fraunces',serif;font-size:20px;font-weight:700}
.modal-close-btn{background:none;border:none;font-size:22px;cursor:pointer;color:var(--muted);line-height:1;padding:2px 6px;border-radius:6px}
.modal-close-btn:hover{background:var(--bg)}
.modal-macros-row{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:14px}
.macro-pill{background:var(--bg);border:1px solid var(--border);border-radius:20px;padding:4px 10px;font-size:12px;color:var(--muted)}
.modal-section{font-size:11px;font-weight:500;text-transform:uppercase;letter-spacing:.07em;color:var(--muted);margin-bottom:6px}
.ingredients-box{background:var(--bg);border-radius:10px;padding:12px 14px;font-size:13px;color:var(--text);line-height:1.7;margin-bottom:14px}
.steps-box{background:var(--bg);border-radius:10px;padding:12px 14px;font-size:13px;color:var(--text);line-height:1.8;margin-bottom:16px;min-height:60px;white-space:pre-line}
.modal-actions{display:flex;gap:8px}
.use-btn{flex:1;background:var(--green);color:#fff;border:none;border-radius:10px;padding:11px;font-size:14px;cursor:pointer;font-family:'DM Sans',sans-serif;font-weight:500;transition:opacity .15s}
.use-btn:hover{opacity:.88}
.meal-select{flex:1;background:var(--bg);border:1px solid var(--border);border-radius:10px;padding:10px;font-size:14px;color:var(--text);font-family:'DM Sans',sans-serif;cursor:pointer;outline:none}
.meal-select:focus{border-color:var(--green-mid)}

/* GOALS */
.goals-card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);padding:20px;box-shadow:var(--shadow);max-width:420px}
.goals-title{font-family:'Fraunces',serif;font-size:18px;font-weight:700;margin-bottom:16px}
.goal-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px}
.goal-label{font-size:14px;color:var(--text);display:flex;align-items:center;gap:8px}
.goal-icon{font-size:16px}
.goal-input{width:90px;text-align:right;font-size:15px;font-weight:500;font-family:'Fraunces',serif;padding:6px 10px;border:1px solid var(--border);border-radius:8px;background:var(--bg);color:var(--text);outline:none;transition:border .15s}
.goal-input:focus{border-color:var(--green-mid)}
.save-goals-btn{background:var(--green);color:#fff;border:none;border-radius:10px;padding:11px 20px;font-size:14px;cursor:pointer;font-family:'DM Sans',sans-serif;font-weight:500;width:100%;margin-top:8px;transition:opacity .15s}
.save-goals-btn:hover{opacity:.88}
.goals-tip{font-size:12px;color:var(--muted);margin-top:10px;text-align:center}

/* LOADING DOTS */
.dots::after{content:'';animation:dotani 1.2s infinite}
@keyframes dotani{0%{content:'.'}40%{content:'..'}80%{content:'...'}}

/* WEEKLY */
.week-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:6px;margin-bottom:1.5rem}
.week-day{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:10px 6px;text-align:center;cursor:pointer;transition:all .15s}
.week-day:hover{border-color:var(--green-mid)}
.week-day.today{border-color:var(--green-mid);background:var(--green-light)}
.week-day.selected{background:var(--green);border-color:var(--green)}
.week-day.selected .wd-name,.week-day.selected .wd-cal{color:#fff}
.wd-name{font-size:11px;color:var(--muted);margin-bottom:4px;font-weight:500}
.wd-num{font-size:16px;font-weight:500;font-family:'Fraunces',serif;color:var(--text)}
.wd-cal{font-size:10px;color:var(--muted);margin-top:3px}

/* RESPONSIVE */
@media(max-width:600px){
  .summary-grid{grid-template-columns:repeat(3,1fr)}
  .stat-val{font-size:22px}
  .add-grid{grid-template-columns:1fr 1fr;gap:5px}
  .add-grid input:first-child{grid-column:1/-1}
  .add-btn{grid-column:1/-1}
  .nav-tabs{display:none}
  .mobile-tabs{display:flex}
  .week-grid{grid-template-columns:repeat(7,1fr)}
  .wd-name{font-size:9px}
  .wd-num{font-size:13px}
}
.mobile-tabs{display:none;position:fixed;bottom:0;left:0;right:0;background:var(--card);border-top:1px solid var(--border);z-index:50}
.mobile-tab{flex:1;padding:12px 4px 16px;display:flex;flex-direction:column;align-items:center;gap:3px;background:none;border:none;cursor:pointer;font-family:'DM Sans',sans-serif;font-size:10px;color:var(--muted);transition:color .15s}
.mobile-tab.active{color:var(--green)}
.mobile-tab-icon{font-size:20px}
@media(max-width:600px){body{padding-bottom:70px}}
</style>
</head>
<body>

<nav>
  <a class="brand" href="#">nourish<span>.</span></a>
  <div class="nav-tabs">
    <button class="nav-tab active" data-tab="planner" id="navPlanner">📋 Planner</button>
    <button class="nav-tab" data-tab="recipes" id="navRecipes">🍽️ Recipes</button>
    <button class="nav-tab" data-tab="goals" id="navGoals">🎯 Goals</button>
  </div>
  <select class="lang-select" id="langSelect">
    <option value="en">🇬🇧 English</option>
    <option value="no">🇳🇴 Norsk</option>
    <option value="es">🇪🇸 Español</option>
    <option value="fr">🇫🇷 Français</option>
    <option value="de">🇩🇪 Deutsch</option>
    <option value="it">🇮🇹 Italiano</option>
    <option value="pt">🇵🇹 Português</option>
    <option value="zh">🇨🇳 中文</option>
    <option value="ja">🇯🇵 日本語</option>
    <option value="ar">🇸🇦 العربية</option>
  </select>
</nav>

<div class="mobile-tabs">
  <button class="mobile-tab active" data-tab="planner"><span class="mobile-tab-icon">📋</span><span id="mtPlanner">Planner</span></button>
  <button class="mobile-tab" data-tab="recipes"><span class="mobile-tab-icon">🍽️</span><span id="mtRecipes">Recipes</span></button>
  <button class="mobile-tab" data-tab="goals"><span class="mobile-tab-icon">🎯</span><span id="mtGoals">Goals</span></button>
</div>

<div class="container">

  <!-- PLANNER -->
  <div class="view active" id="view-planner">
    <div class="week-grid" id="weekGrid"></div>
    <div class="date-row">
      <button class="date-btn" id="prevDay">‹</button>
      <div class="date-label" id="dateLabel">Today</div>
      <button class="date-btn" id="nextDay">›</button>
    </div>
    <div class="summary-grid">
      <div class="stat-card">
        <div class="stat-label" data-i18n="calories">Calories</div>
        <div><span class="stat-val" id="totalCal">0</span></div>
        <div class="stat-sub"><span id="calLeft">2000</span> <span data-i18n="remaining">remaining</span></div>
        <div class="progress-bar"><div class="progress-fill cal-fill" id="calBar" style="width:0%"></div></div>
      </div>
      <div class="stat-card">
        <div class="stat-label" data-i18n="protein">Protein</div>
        <div><span class="stat-val" id="totalProt">0</span><span class="stat-unit">g</span></div>
        <div class="stat-sub"><span data-i18n="goal">Goal</span>: <span id="protGoalShow">150</span>g</div>
        <div class="progress-bar"><div class="progress-fill prot-fill" id="protBar" style="width:0%"></div></div>
      </div>
      <div class="stat-card">
        <div class="stat-label" data-i18n="carbs">Carbs</div>
        <div><span class="stat-val" id="totalCarb">0</span><span class="stat-unit">g</span></div>
        <div class="stat-sub"><span data-i18n="goal">Goal</span>: <span id="carbGoalShow">250</span>g</div>
        <div class="progress-bar"><div class="progress-fill carb-fill" id="carbBar" style="width:0%"></div></div>
      </div>
    </div>
    <div class="meals-wrap" id="mealsWrap"></div>
  </div>

  <!-- RECIPES -->
  <div class="view" id="view-recipes">
    <div class="section-title" id="recipeTitle">Recipes</div>
    <div style="display:flex;gap:8px;margin-bottom:12px;flex-wrap:wrap;align-items:center">
      <input type="text" id="recipeSearch" placeholder="Search recipes..." style="flex:1;min-width:140px;font-size:13px;padding:8px 12px;border:1px solid var(--border);border-radius:10px;background:var(--card);color:var(--text);font-family:'DM Sans',sans-serif;outline:none">
      <select id="recipeFilter" style="font-size:13px;padding:8px 12px;border:1px solid var(--border);border-radius:10px;background:var(--card);color:var(--text);font-family:'DM Sans',sans-serif;cursor:pointer;outline:none">
        <option value="all">All categories</option>
        <option value="breakfast">🌅 Breakfast</option>
        <option value="high-protein">💪 High Protein</option>
        <option value="low-carb">🥬 Low Carb</option>
        <option value="veggie">🌿 Veggie</option>
        <option value="seafood">🐟 Seafood</option>
        <option value="world">🌍 World</option>
        <option value="quick">⚡ Quick</option>
        <option value="soup">🍲 Soups</option>
        <option value="salad">🥗 Salads</option>
        <option value="pasta">🍝 Pasta</option>
        <option value="snack">🍎 Snacks</option>
        <option value="chicken">🍗 Chicken</option>
        <option value="beef">🥩 Beef & Pork</option>
        <option value="plant-based">🌱 Plant-Based</option>
      </select>
    </div>
    <div style="font-size:12px;color:var(--muted);margin-bottom:10px" id="recipeCount"></div>
    <div class="recipe-grid" id="recipeGrid"></div>
  </div>

  <!-- GOALS -->
  <div class="view" id="view-goals">
    <div class="goals-card">
      <div class="goals-title" data-i18n="dailyGoals">Daily Goals</div>
      <div class="goal-row">
        <div class="goal-label"><span class="goal-icon">🔥</span><span data-i18n="calorieGoal">Calorie Goal</span></div>
        <input class="goal-input" type="number" id="gCal" value="2000">
      </div>
      <div class="goal-row">
        <div class="goal-label"><span class="goal-icon">💪</span><span data-i18n="proteinGoal">Protein (g)</span></div>
        <input class="goal-input" type="number" id="gProt" value="150">
      </div>
      <div class="goal-row">
        <div class="goal-label"><span class="goal-icon">🌾</span><span data-i18n="carbGoal">Carbs (g)</span></div>
        <input class="goal-input" type="number" id="gCarb" value="250">
      </div>
      <div class="goal-row">
        <div class="goal-label"><span class="goal-icon">🥑</span><span data-i18n="fatGoal">Fat (g)</span></div>
        <input class="goal-input" type="number" id="gFat" value="65">
      </div>
      <button class="save-goals-btn" id="saveGoalsBtn" data-i18n="saveGoals">Save Goals</button>
      <div class="goals-tip" data-i18n="goalsTip">Goals are saved in your browser</div>
    </div>
  </div>
</div>

<!-- RECIPE MODAL -->
<div class="modal-bg" id="recipeModal">
  <div class="modal">
    <div class="modal-top">
      <div class="modal-title" id="mTitle"></div>
      <button class="modal-close-btn" id="mClose">×</button>
    </div>
    <div class="modal-macros-row" id="mMacros"></div>
    <div class="modal-section" data-i18n="ingredients">Ingredients</div>
    <div class="ingredients-box" id="mIngredients"></div>
    <div class="modal-section" data-i18n="steps">Steps</div>
    <div class="steps-box" id="mSteps"><span class="dots">Loading</span></div>
    <div class="modal-actions">
      <select class="meal-select" id="mMealSelect"></select>
      <button class="use-btn" id="mUseBtn" data-i18n="addToMeal">Add to Meal</button>
    </div>
  </div>
</div>

<script>
// ─── I18N ────────────────────────────────────────────────────────────────────
const T={
  en:{calories:'Calories',protein:'Protein',carbs:'Carbs',remaining:'remaining',goal:'Goal',today:'Today',dailyGoals:'Daily Goals',calorieGoal:'Calorie Goal',proteinGoal:'Protein (g)',carbGoal:'Carbs (g)',fatGoal:'Fat (g)',saveGoals:'Save Goals',goalsTip:'Goals saved in your browser',addToMeal:'Add to Meal',ingredients:'Ingredients',steps:'How to make it',recipes:'Recipes',breakfast:'Breakfast',lunch:'Lunch',dinner:'Dinner',snacks:'Snacks',addFood:'Food name...',kcal:'kcal',prot:'Protein',carb:'Carbs',addBtn:'Add',aiSuggest:'Suggest meal with AI',loading:'Loading',planner:'Planner',goals:'Goals',fat:'Fat',mon:'Mon',tue:'Tue',wed:'Wed',thu:'Thu',fri:'Fri',sat:'Sat',sun:'Sun'},
  no:{calories:'Kalorier',protein:'Protein',carbs:'Karbohydrater',remaining:'igjen',goal:'Mål',today:'I dag',dailyGoals:'Daglige mål',calorieGoal:'Kalori-mål',proteinGoal:'Protein (g)',carbGoal:'Karbohydrat (g)',fatGoal:'Fett (g)',saveGoals:'Lagre mål',goalsTip:'Mål lagret i nettleseren',addToMeal:'Legg til i måltid',ingredients:'Ingredienser',steps:'Fremgangsmåte',recipes:'Oppskrifter',breakfast:'Frokost',lunch:'Lunsj',dinner:'Middag',snacks:'Snacks',addFood:'Matnavn...',kcal:'kcal',prot:'Protein',carb:'Karbo',addBtn:'Legg til',aiSuggest:'Foreslå måltid med AI',loading:'Laster',planner:'Planlegger',goals:'Mål',fat:'Fett',mon:'Man',tue:'Tir',wed:'Ons',thu:'Tor',fri:'Fre',sat:'Lør',sun:'Søn'},
  es:{calories:'Calorías',protein:'Proteína',carbs:'Carbohidratos',remaining:'restantes',goal:'Meta',today:'Hoy',dailyGoals:'Metas diarias',calorieGoal:'Meta calórica',proteinGoal:'Proteína (g)',carbGoal:'Carbos (g)',fatGoal:'Grasa (g)',saveGoals:'Guardar metas',goalsTip:'Metas guardadas en el navegador',addToMeal:'Añadir a comida',ingredients:'Ingredientes',steps:'Preparación',recipes:'Recetas',breakfast:'Desayuno',lunch:'Almuerzo',dinner:'Cena',snacks:'Snacks',addFood:'Nombre del alimento...',kcal:'kcal',prot:'Proteína',carb:'Carbs',addBtn:'Añadir',aiSuggest:'Sugerir comida con IA',loading:'Cargando',planner:'Planificador',goals:'Metas',fat:'Grasa',mon:'Lun',tue:'Mar',wed:'Mié',thu:'Jue',fri:'Vie',sat:'Sáb',sun:'Dom'},
  fr:{calories:'Calories',protein:'Protéines',carbs:'Glucides',remaining:'restantes',goal:'Objectif',today:"Aujourd'hui",dailyGoals:'Objectifs journaliers',calorieGoal:'Objectif calorique',proteinGoal:'Protéines (g)',carbGoal:'Glucides (g)',fatGoal:'Lipides (g)',saveGoals:'Sauvegarder',goalsTip:'Objectifs enregistrés',addToMeal:'Ajouter au repas',ingredients:'Ingrédients',steps:'Préparation',recipes:'Recettes',breakfast:'Petit-déjeuner',lunch:'Déjeuner',dinner:'Dîner',snacks:'Snacks',addFood:'Nom de l\'aliment...',kcal:'kcal',prot:'Protéines',carb:'Glucides',addBtn:'Ajouter',aiSuggest:'Suggérer un repas IA',loading:'Chargement',planner:'Planificateur',goals:'Objectifs',fat:'Lipides',mon:'Lun',tue:'Mar',wed:'Mer',thu:'Jeu',fri:'Ven',sat:'Sam',sun:'Dim'},
  de:{calories:'Kalorien',protein:'Protein',carbs:'Kohlenhydrate',remaining:'übrig',goal:'Ziel',today:'Heute',dailyGoals:'Tagesziele',calorieGoal:'Kalorienziel',proteinGoal:'Protein (g)',carbGoal:'Kohlenhydrate (g)',fatGoal:'Fett (g)',saveGoals:'Ziele speichern',goalsTip:'Ziele im Browser gespeichert',addToMeal:'Zur Mahlzeit hinzufügen',ingredients:'Zutaten',steps:'Zubereitung',recipes:'Rezepte',breakfast:'Frühstück',lunch:'Mittagessen',dinner:'Abendessen',snacks:'Snacks',addFood:'Lebensmittel...',kcal:'kcal',prot:'Protein',carb:'Kohlenhydrate',addBtn:'Hinzufügen',aiSuggest:'Mahlzeit mit KI vorschlagen',loading:'Laden',planner:'Planer',goals:'Ziele',fat:'Fett',mon:'Mo',tue:'Di',wed:'Mi',thu:'Do',fri:'Fr',sat:'Sa',sun:'So'},
  it:{calories:'Calorie',protein:'Proteine',carbs:'Carboidrati',remaining:'rimanenti',goal:'Obiettivo',today:'Oggi',dailyGoals:'Obiettivi giornalieri',calorieGoal:'Obiettivo calorie',proteinGoal:'Proteine (g)',carbGoal:'Carboidrati (g)',fatGoal:'Grassi (g)',saveGoals:'Salva obiettivi',goalsTip:'Obiettivi salvati nel browser',addToMeal:'Aggiungi al pasto',ingredients:'Ingredienti',steps:'Preparazione',recipes:'Ricette',breakfast:'Colazione',lunch:'Pranzo',dinner:'Cena',snacks:'Spuntino',addFood:'Nome alimento...',kcal:'kcal',prot:'Proteine',carb:'Carboidrati',addBtn:'Aggiungi',aiSuggest:'Suggerisci pasto con IA',loading:'Caricamento',planner:'Pianificatore',goals:'Obiettivi',fat:'Grassi',mon:'Lun',tue:'Mar',wed:'Mer',thu:'Gio',fri:'Ven',sat:'Sab',sun:'Dom'},
  pt:{calories:'Calorias',protein:'Proteína',carbs:'Carboidratos',remaining:'restantes',goal:'Meta',today:'Hoje',dailyGoals:'Metas diárias',calorieGoal:'Meta calórica',proteinGoal:'Proteína (g)',carbGoal:'Carboidratos (g)',fatGoal:'Gordura (g)',saveGoals:'Salvar metas',goalsTip:'Metas salvas no navegador',addToMeal:'Adicionar à refeição',ingredients:'Ingredientes',steps:'Preparo',recipes:'Receitas',breakfast:'Café da manhã',lunch:'Almoço',dinner:'Jantar',snacks:'Lanches',addFood:'Nome do alimento...',kcal:'kcal',prot:'Proteína',carb:'Carbs',addBtn:'Adicionar',aiSuggest:'Sugerir refeição com IA',loading:'Carregando',planner:'Planejador',goals:'Metas',fat:'Gordura',mon:'Seg',tue:'Ter',wed:'Qua',thu:'Qui',fri:'Sex',sat:'Sáb',sun:'Dom'},
  zh:{calories:'卡路里',protein:'蛋白质',carbs:'碳水化合物',remaining:'剩余',goal:'目标',today:'今天',dailyGoals:'每日目标',calorieGoal:'卡路里目标',proteinGoal:'蛋白质 (g)',carbGoal:'碳水 (g)',fatGoal:'脂肪 (g)',saveGoals:'保存目标',goalsTip:'目标已保存至浏览器',addToMeal:'添加到餐食',ingredients:'食材',steps:'做法',recipes:'食谱',breakfast:'早餐',lunch:'午餐',dinner:'晚餐',snacks:'零食',addFood:'食物名称...',kcal:'千卡',prot:'蛋白质',carb:'碳水',addBtn:'添加',aiSuggest:'AI推荐餐食',loading:'加载中',planner:'计划',goals:'目标',fat:'脂肪',mon:'周一',tue:'周二',wed:'周三',thu:'周四',fri:'周五',sat:'周六',sun:'周日'},
  ja:{calories:'カロリー',protein:'タンパク質',carbs:'炭水化物',remaining:'残り',goal:'目標',today:'今日',dailyGoals:'1日の目標',calorieGoal:'カロリー目標',proteinGoal:'タンパク質 (g)',carbGoal:'炭水化物 (g)',fatGoal:'脂質 (g)',saveGoals:'目標を保存',goalsTip:'目標はブラウザに保存されます',addToMeal:'食事に追加',ingredients:'材料',steps:'作り方',recipes:'レシピ',breakfast:'朝食',lunch:'昼食',dinner:'夕食',snacks:'スナック',addFood:'食品名...',kcal:'kcal',prot:'タンパク質',carb:'炭水化物',addBtn:'追加',aiSuggest:'AIで食事提案',loading:'読み込み中',planner:'プランナー',goals:'目標',fat:'脂質',mon:'月',tue:'火',wed:'水',thu:'木',fri:'金',sat:'土',sun:'日'},
  ar:{calories:'سعرات',protein:'بروتين',carbs:'كربوهيدرات',remaining:'متبقية',goal:'هدف',today:'اليوم',dailyGoals:'الأهداف اليومية',calorieGoal:'هدف السعرات',proteinGoal:'البروتين (g)',carbGoal:'الكربوهيدرات (g)',fatGoal:'الدهون (g)',saveGoals:'حفظ الأهداف',goalsTip:'تم حفظ الأهداف في المتصفح',addToMeal:'إضافة لوجبة',ingredients:'المكونات',steps:'طريقة التحضير',recipes:'وصفات',breakfast:'فطور',lunch:'غداء',dinner:'عشاء',snacks:'وجبات خفيفة',addFood:'اسم الطعام...',kcal:'سعرة',prot:'بروتين',carb:'كارب',addBtn:'إضافة',aiSuggest:'اقتراح وجبة بالذكاء الاصطناعي',loading:'جار التحميل',planner:'المخطط',goals:'الأهداف',fat:'دهون',mon:'الإث',tue:'الثل',wed:'الأر',thu:'الخم',fri:'الجم',sat:'السب',sun:'الأح'}
};
function t(k){return(T[lang]||T.en)[k]||k}

// ─── STATE ───────────────────────────────────────────────────────────────────
let lang='en';
let goals={cal:2000,prot:150,carb:250,fat:65};
let dayOffset=0;
let allDays={};
let currentRecipeIdx=null;
const mealKeys=['breakfast','lunch','dinner','snacks'];
const mealMeta={
  breakfast:{icon:'🌅',bg:'#fff8e1'},
  lunch:{icon:'☀️',bg:'#e8f5e9'},
  dinner:{icon:'🌙',bg:'#ede7f6'},
  snacks:{icon:'🍎',bg:'#fce4ec'}
};
const recipes=[
  // BREAKFAST
  {emoji:'🥑',name:'Avocado Toast',cal:380,prot:14,carb:32,fat:22,tag:'breakfast',ingredients:'2 slices sourdough bread, 1 ripe avocado, 2 eggs (poached or fried), salt, black pepper, red chili flakes, lemon juice'},
  {emoji:'🥣',name:'Protein Oats',cal:420,prot:28,carb:52,fat:10,tag:'breakfast',ingredients:'80g rolled oats, 1 scoop vanilla protein powder (30g), 1 banana, 200ml almond milk, 1 tbsp honey, pinch cinnamon'},
  {emoji:'🍳',name:'Veggie Omelette',cal:320,prot:22,carb:4,fat:24,tag:'breakfast',ingredients:'3 large eggs, 1 cup baby spinach, 100g mushrooms, 30g cheddar, 1 tbsp butter, salt, pepper'},
  {emoji:'🫐',name:'Berry Smoothie Bowl',cal:340,prot:18,carb:48,fat:8,tag:'breakfast',ingredients:'1 cup frozen mixed berries, 1 banana, 150g Greek yogurt, 1 scoop protein powder, granola, chia seeds, fresh berries to top'},
  {emoji:'🥞',name:'Protein Pancakes',cal:410,prot:30,carb:44,fat:10,tag:'breakfast',ingredients:'2 bananas, 2 eggs, 1 scoop protein powder, 1 tsp baking powder, pinch salt, 1 tsp vanilla, coconut oil for cooking, maple syrup'},
  {emoji:'🍌',name:'Banana Nut Overnight Oats',cal:390,prot:16,carb:58,fat:12,tag:'breakfast',ingredients:'80g oats, 200ml oat milk, 1 banana, 2 tbsp peanut butter, 1 tbsp chia seeds, 1 tsp honey, pinch cinnamon'},
  {emoji:'🥚',name:'Egg & Veggie Scramble',cal:300,prot:24,carb:8,fat:20,tag:'breakfast',ingredients:'3 eggs, 1 bell pepper, ½ onion, 1 cup spinach, 2 tbsp olive oil, salt, pepper, paprika, fresh herbs'},
  {emoji:'🧇',name:'French Toast',cal:430,prot:16,carb:52,fat:18,tag:'breakfast',ingredients:'3 thick slices brioche, 2 eggs, 100ml milk, 1 tsp vanilla, 1 tsp cinnamon, 1 tbsp butter, maple syrup, fresh berries'},
  {emoji:'🍓',name:'Yogurt Parfait',cal:310,prot:20,carb:42,fat:6,tag:'breakfast',ingredients:'200g Greek yogurt, 1 cup mixed berries, 4 tbsp granola, 1 tbsp honey, 1 tbsp chia seeds'},
  {emoji:'🫓',name:'Cottage Cheese Toast',cal:290,prot:22,carb:26,fat:10,tag:'breakfast',ingredients:'2 slices wholegrain toast, 150g cottage cheese, cucumber slices, cherry tomatoes, fresh dill, salt, black pepper, drizzle olive oil'},
  {emoji:'🥤',name:'Green Protein Smoothie',cal:350,prot:26,carb:40,fat:8,tag:'breakfast',ingredients:'2 cups spinach, 1 banana, 1 scoop vanilla protein powder, 200ml almond milk, 1 tbsp almond butter, ½ tsp ginger'},
  {emoji:'🍞',name:'Peanut Butter Banana Toast',cal:440,prot:18,carb:54,fat:18,tag:'breakfast',ingredients:'2 slices wholegrain bread, 2 tbsp natural peanut butter, 1 banana sliced, 1 tsp honey, pinch cinnamon'},
  // HIGH PROTEIN
  {emoji:'🍗',name:'Grilled Chicken Bowl',cal:520,prot:48,carb:38,fat:12,tag:'high-protein',ingredients:'200g chicken breast, 100g cooked rice, 2 cups mixed greens, 2 tbsp olive oil, juice of 1 lemon, 2 cloves garlic, salt, pepper'},
  {emoji:'🍣',name:'Salmon Teriyaki Bowl',cal:560,prot:42,carb:44,fat:20,tag:'high-protein',ingredients:'200g salmon fillet, 150g cooked rice, 2 tbsp soy sauce, 1 tbsp mirin, 1 tbsp honey, sesame seeds, spring onion, cucumber'},
  {emoji:'🥩',name:'Beef Stir-fry',cal:580,prot:44,carb:34,fat:28,tag:'high-protein',ingredients:'200g beef sirloin strips, 2 cups broccoli, 1 bell pepper, 3 tbsp soy sauce, 1 tbsp oyster sauce, garlic, ginger, sesame oil, 100g noodles'},
  {emoji:'🫔',name:'Turkey Wrap',cal:460,prot:36,carb:42,fat:14,tag:'high-protein',ingredients:'1 large whole-wheat tortilla, 150g sliced turkey breast, 2 tbsp hummus, romaine lettuce, tomato, cucumber, red onion, mustard'},
  {emoji:'🍱',name:'Tuna Rice Bowl',cal:490,prot:44,carb:48,fat:10,tag:'high-protein',ingredients:'2 cans tuna in water, 150g cooked brown rice, 1 avocado, edamame, cucumber, soy sauce, sesame oil, sriracha'},
  {emoji:'🐟',name:'Baked Cod with Quinoa',cal:440,prot:46,carb:36,fat:10,tag:'high-protein',ingredients:'200g cod fillet, 120g quinoa, cherry tomatoes, lemon zest, garlic, olive oil, fresh parsley, salt, pepper'},
  {emoji:'🥚',name:'Egg White Frittata',cal:280,prot:32,carb:6,fat:12,tag:'high-protein',ingredients:'6 egg whites, 1 whole egg, 100g turkey ham, 1 cup spinach, 50g feta, cherry tomatoes, olive oil, herbs'},
  {emoji:'🍖',name:'Pork Tenderloin & Veg',cal:510,prot:46,carb:22,fat:24,tag:'high-protein',ingredients:'220g pork tenderloin, 200g roasted sweet potato, green beans, 1 tbsp olive oil, rosemary, garlic, mustard, salt'},
  {emoji:'🦃',name:'Turkey Meatball Bowl',cal:530,prot:42,carb:46,fat:16,tag:'high-protein',ingredients:'250g minced turkey, 1 egg, breadcrumbs, garlic, 150g pasta, marinara sauce, parmesan, fresh basil'},
  {emoji:'🐔',name:'Chicken Shawarma Bowl',cal:540,prot:44,carb:42,fat:18,tag:'high-protein',ingredients:'200g chicken thigh, cumin, coriander, turmeric, garlic, lemon, 150g rice, tzatziki, tomato, cucumber, flatbread'},
  // LOW CARB
  {emoji:'🥗',name:'Greek Salad',cal:290,prot:11,carb:18,fat:20,tag:'low-carb',ingredients:'1 cucumber, 3 tomatoes, 100g feta cheese, handful olives, ½ red onion, 3 tbsp olive oil, 1 tsp dried oregano, salt'},
  {emoji:'🥬',name:'Zucchini Noodle Bolognese',cal:380,prot:28,carb:14,fat:22,tag:'low-carb',ingredients:'3 medium zucchinis (spiralized), 200g lean beef mince, 1 can crushed tomatoes, onion, garlic, tomato paste, olive oil, basil'},
  {emoji:'🥦',name:'Cauliflower Fried Rice',cal:320,prot:18,carb:20,fat:16,tag:'low-carb',ingredients:'1 head cauliflower (riced), 2 eggs, 150g shrimp, 1 cup peas, soy sauce, sesame oil, garlic, ginger, spring onion'},
  {emoji:'🥩',name:'Steak & Asparagus',cal:480,prot:44,carb:8,fat:30,tag:'low-carb',ingredients:'200g sirloin steak, 200g asparagus, 2 tbsp butter, garlic, thyme, lemon, salt, pepper, olive oil'},
  {emoji:'🍗',name:'Lemon Herb Chicken Thighs',cal:430,prot:40,carb:4,fat:28,tag:'low-carb',ingredients:'4 chicken thighs (skin-on), lemon zest & juice, fresh thyme, rosemary, garlic, olive oil, salt, pepper'},
  {emoji:'🥒',name:'Caprese Salad',cal:260,prot:14,carb:8,fat:20,tag:'low-carb',ingredients:'3 large tomatoes, 200g fresh mozzarella, fresh basil leaves, 3 tbsp extra virgin olive oil, balsamic glaze, salt, pepper'},
  {emoji:'🐟',name:'Tuna Stuffed Avocado',cal:340,prot:28,carb:10,fat:22,tag:'low-carb',ingredients:'2 avocados, 2 cans tuna, 2 tbsp mayo, celery, red onion, lemon juice, salt, pepper, paprika'},
  {emoji:'🥚',name:'Shakshuka',cal:360,prot:20,carb:22,fat:22,tag:'low-carb',ingredients:'4 eggs, 1 can crushed tomatoes, 1 red pepper, onion, garlic, cumin, paprika, chili, feta, fresh parsley, olive oil'},
  // VEGGIE
  {emoji:'🍝',name:'Pasta Primavera',cal:480,prot:16,carb:72,fat:14,tag:'veggie',ingredients:'200g pasta (penne or fusilli), 1 zucchini, 200g cherry tomatoes, 3 garlic cloves, 3 tbsp olive oil, 40g parmesan, fresh basil, salt'},
  {emoji:'🌮',name:'Black Bean Tacos',cal:440,prot:18,carb:58,fat:16,tag:'veggie',ingredients:'2 corn tortillas, 1 can black beans, ½ avocado, salsa, lime juice, cumin, smoked paprika, coriander, red cabbage'},
  {emoji:'🍲',name:'Lentil Soup',cal:380,prot:22,carb:52,fat:8,tag:'veggie',ingredients:'200g red lentils, 1 onion, 2 carrots, 2 garlic cloves, 1 tsp cumin, 1 tsp turmeric, 400ml vegetable stock, 1 can diced tomatoes, olive oil'},
  {emoji:'🫘',name:'Chickpea Curry',cal:460,prot:18,carb:62,fat:14,tag:'veggie',ingredients:'2 cans chickpeas, 1 can coconut milk, 1 can crushed tomatoes, onion, garlic, ginger, garam masala, cumin, coriander, turmeric, rice to serve'},
  {emoji:'🌯',name:'Falafel Wrap',cal:490,prot:16,carb:66,fat:18,tag:'veggie',ingredients:'6 falafel balls, 1 large wrap, hummus, tahini, cucumber, tomato, red onion, mixed lettuce, lemon juice'},
  {emoji:'🍕',name:'Veggie Flatbread Pizza',cal:420,prot:18,carb:54,fat:16,tag:'veggie',ingredients:'1 flatbread, 3 tbsp tomato sauce, 80g mozzarella, zucchini, roasted red pepper, olives, fresh basil, olive oil'},
  {emoji:'🧆',name:'Lentil Dahl',cal:400,prot:20,carb:58,fat:10,tag:'veggie',ingredients:'200g red lentils, 1 can coconut milk, onion, garlic, ginger, curry powder, cumin seeds, turmeric, spinach, naan bread'},
  {emoji:'🥘',name:'Ratatouille',cal:280,prot:8,carb:34,fat:12,tag:'veggie',ingredients:'1 eggplant, 2 zucchinis, 3 tomatoes, 1 yellow pepper, onion, garlic, fresh thyme, rosemary, olive oil, tomato passata'},
  {emoji:'🌽',name:'Sweet Corn Chowder',cal:360,prot:10,carb:54,fat:12,tag:'veggie',ingredients:'3 ears corn, 2 potatoes, 1 onion, 2 garlic cloves, 500ml vegetable stock, 100ml cream, butter, chives, salt, pepper'},
  {emoji:'🥙',name:'Halloumi & Veg Wrap',cal:470,prot:22,carb:48,fat:22,tag:'veggie',ingredients:'100g halloumi, 1 large wrap, roasted red pepper, zucchini, hummus, spinach, sun-dried tomatoes, lemon, olive oil'},
  // SEAFOOD
  {emoji:'🦐',name:'Prawn & Mango Salad',cal:320,prot:26,carb:30,fat:10,tag:'seafood',ingredients:'200g cooked prawns, 1 mango (diced), mixed greens, cucumber, red onion, avocado, lime juice, fish sauce, chili, fresh mint'},
  {emoji:'🐡',name:'Fish Tacos',cal:480,prot:30,carb:52,fat:16,tag:'seafood',ingredients:'200g white fish (cod or tilapia), 2 corn tortillas, lime, cumin, smoked paprika, cabbage slaw, sour cream, avocado, salsa'},
  {emoji:'🦞',name:'Garlic Butter Shrimp Pasta',cal:540,prot:32,carb:58,fat:18,tag:'seafood',ingredients:'200g shrimp, 180g linguine, 4 garlic cloves, 3 tbsp butter, white wine, lemon juice, parsley, chili flakes, parmesan'},
  {emoji:'🐠',name:'Seared Tuna Steak',cal:380,prot:48,carb:8,fat:16,tag:'seafood',ingredients:'200g sushi-grade tuna, sesame seeds, soy sauce, ginger, 1 tsp sesame oil, green beans, edamame, lemon'},
  {emoji:'🦀',name:'Crab Cakes',cal:420,prot:28,carb:28,fat:20,tag:'seafood',ingredients:'250g crab meat, breadcrumbs, 1 egg, mayo, Dijon mustard, lemon, spring onion, chili, oil for frying, salad to serve'},
  {emoji:'🐙',name:'Prawn Pad Thai',cal:520,prot:30,carb:62,fat:14,tag:'seafood',ingredients:'200g prawns, 150g rice noodles, 2 eggs, 3 tbsp fish sauce, 2 tbsp lime juice, 1 tbsp sugar, bean sprouts, spring onion, peanuts, chili'},
  // WORLD CUISINE
  {emoji:'🍜',name:'Chicken Ramen',cal:560,prot:38,carb:58,fat:18,tag:'world',ingredients:'2 chicken thighs, 100g ramen noodles, 4 cups chicken broth, soy sauce, mirin, 2 soft-boiled eggs, nori, spring onion, corn, bamboo shoots'},
  {emoji:'🥘',name:'Beef Tagine',cal:580,prot:40,carb:44,fat:22,tag:'world',ingredients:'300g beef chuck, 1 can chickpeas, dried apricots, 1 onion, garlic, ginger, cumin, coriander, turmeric, cinnamon, vegetable stock, couscous'},
  {emoji:'🍛',name:'Butter Chicken',cal:560,prot:38,carb:36,fat:26,tag:'world',ingredients:'300g chicken breast, 1 can crushed tomatoes, 100ml cream, butter, onion, garlic, ginger, garam masala, cumin, coriander, basmati rice'},
  {emoji:'🫕',name:'Shakshuka',cal:360,prot:20,carb:22,fat:22,tag:'world',ingredients:'4 eggs, 1 can crushed tomatoes, 1 red pepper, onion, garlic, cumin, paprika, harissa, feta, parsley, crusty bread'},
  {emoji:'🍚',name:'Bibimbap',cal:520,prot:26,carb:68,fat:14,tag:'world',ingredients:'150g short-grain rice, 100g beef mince, carrots, zucchini, spinach, bean sprouts, fried egg, gochujang, sesame oil, soy sauce'},
  {emoji:'🥗',name:'Thai Beef Salad',cal:380,prot:32,carb:18,fat:20,tag:'world',ingredients:'200g grilled beef, mixed herbs (mint, coriander, basil), cherry tomatoes, cucumber, red onion, fish sauce, lime juice, chili, toasted rice'},
  {emoji:'🫙',name:'Hummus Bowl',cal:390,prot:14,carb:48,fat:16,tag:'world',ingredients:'200g hummus, roasted chickpeas, roasted red pepper, cucumber, cherry tomatoes, olives, zaatar, olive oil, warm pitta bread'},
  {emoji:'🍣',name:'Poke Bowl',cal:490,prot:34,carb:54,fat:14,tag:'world',ingredients:'150g sushi-grade salmon or tuna, 150g sushi rice, edamame, cucumber, mango, avocado, soy sauce, sesame oil, ginger, sesame seeds, sriracha mayo'},
  {emoji:'🌯',name:'Souvlaki Wrap',cal:520,prot:36,carb:52,fat:18,tag:'world',ingredients:'200g pork tenderloin, pita bread, tzatziki, tomato, red onion, lettuce, lemon, oregano, garlic, olive oil'},
  {emoji:'🍜',name:'Pho Soup',cal:440,prot:34,carb:48,fat:10,tag:'world',ingredients:'150g rice noodles, 200g beef slices, 1 litre beef broth, star anise, cinnamon, ginger, fish sauce, bean sprouts, basil, lime, chili, hoisin sauce'},
  // QUICK & EASY
  {emoji:'🥪',name:'Smashed Chickpea Sandwich',cal:420,prot:18,carb:58,fat:14,tag:'quick',ingredients:'1 can chickpeas, 2 tbsp mayo, 1 tsp Dijon, lemon juice, celery, red onion, dill, salt, pepper, 2 slices wholegrain bread, lettuce, tomato'},
  {emoji:'🥗',name:'Cobb Salad',cal:450,prot:34,carb:12,fat:30,tag:'quick',ingredients:'2 chicken breasts (grilled), 4 eggs (hard-boiled), avocado, bacon, cherry tomatoes, blue cheese, romaine lettuce, ranch dressing'},
  {emoji:'🍳',name:'Fried Rice',cal:460,prot:18,carb:64,fat:14,tag:'quick',ingredients:'2 cups cooked rice (day-old), 2 eggs, 100g mixed veg (peas, corn, carrot), soy sauce, sesame oil, garlic, ginger, spring onion'},
  {emoji:'🥫',name:'Bean & Veggie Soup',cal:330,prot:16,carb:50,fat:6,tag:'quick',ingredients:'1 can cannellini beans, 1 can diced tomatoes, carrot, celery, onion, garlic, vegetable stock, kale, olive oil, rosemary, parmesan rind'},
  {emoji:'🫓',name:'BLT Sandwich',cal:420,prot:22,carb:40,fat:20,tag:'quick',ingredients:'2 slices toasted sourdough, 4 rashers crispy bacon, 2 tomatoes, romaine lettuce, 2 tbsp mayo, salt, pepper'},
  {emoji:'🌯',name:'Caesar Wrap',cal:450,prot:28,carb:38,fat:22,tag:'quick',ingredients:'1 large wrap, 150g grilled chicken, romaine lettuce, caesar dressing, parmesan, croutons, lemon juice, black pepper'},
  {emoji:'🍱',name:'Snack Box',cal:380,prot:22,carb:32,fat:18,tag:'quick',ingredients:'2 hard-boiled eggs, 30g almonds, 50g hummus, carrot sticks, cucumber sticks, 5 cherry tomatoes, 1 rice cake, 30g cheddar'},
  {emoji:'🥐',name:'Ham & Cheese Croissant',cal:430,prot:20,carb:38,fat:22,tag:'quick',ingredients:'1 butter croissant, 60g sliced ham, 40g gruyere cheese, 1 tsp Dijon mustard, fresh chives'},
  // SOUPS & STEWS
  {emoji:'🍜',name:'Chicken Noodle Soup',cal:380,prot:30,carb:38,fat:10,tag:'soup',ingredients:'2 chicken breasts, 100g egg noodles, 2 carrots, 2 celery sticks, onion, garlic, chicken stock, thyme, bay leaf, fresh parsley'},
  {emoji:'🥣',name:'Tomato Basil Soup',cal:240,prot:6,carb:32,fat:10,tag:'soup',ingredients:'1kg ripe tomatoes, 1 onion, 4 garlic cloves, vegetable stock, 100ml cream, fresh basil, olive oil, sugar, salt, pepper, crusty bread'},
  {emoji:'🍲',name:'Minestrone',cal:320,prot:14,carb:50,fat:8,tag:'soup',ingredients:'1 can borlotti beans, pasta, carrot, celery, zucchini, tomatoes, onion, garlic, vegetable stock, kale, olive oil, parmesan'},
  {emoji:'🥘',name:'Beef Bone Broth Stew',cal:480,prot:38,carb:34,fat:20,tag:'soup',ingredients:'300g beef chuck, 2 potatoes, 2 carrots, onion, garlic, beef stock, tomato paste, rosemary, thyme, bay leaf, red wine'},
  {emoji:'🍛',name:'Mulligatawny Soup',cal:360,prot:22,carb:42,fat:12,tag:'soup',ingredients:'200g chicken, red lentils, apple, onion, carrot, garlic, curry powder, coconut milk, chicken stock, lemon juice, rice'},
  {emoji:'🌶️',name:'Sweet Potato & Lentil Soup',cal:340,prot:14,carb:56,fat:8,tag:'soup',ingredients:'2 sweet potatoes, 150g red lentils, 1 can coconut milk, onion, garlic, ginger, cumin, coriander, turmeric, vegetable stock'},
  // SALADS
  {emoji:'🥗',name:'Nicoise Salad',cal:420,prot:30,carb:22,fat:24,tag:'salad',ingredients:'2 tuna fillets (seared), green beans, 3 eggs (boiled), olives, cherry tomatoes, new potatoes, anchovies, Dijon vinaigrette'},
  {emoji:'🫑',name:'Quinoa Power Salad',cal:390,prot:16,carb:52,fat:14,tag:'salad',ingredients:'150g quinoa, roasted butternut squash, 1 can chickpeas, spinach, red onion, pomegranate seeds, feta, tahini dressing, pepitas'},
  {emoji:'🥦',name:'Broccoli Caesar',cal:360,prot:22,carb:20,fat:22,tag:'salad',ingredients:'2 heads broccoli (roasted), anchovy caesar dressing, sourdough croutons, parmesan shavings, lemon, black pepper, capers'},
  {emoji:'🍅',name:'Watermelon Feta Salad',cal:280,prot:10,carb:34,fat:12,tag:'salad',ingredients:'½ small watermelon, 150g feta, mint leaves, cucumber, red onion, rocket, balsamic glaze, olive oil, black pepper'},
  {emoji:'🥑',name:'Mango Avocado Salad',cal:320,prot:8,carb:38,fat:18,tag:'salad',ingredients:'2 mangos, 2 avocados, red onion, cherry tomatoes, lime juice, coriander, jalapeño, olive oil, salt, mixed greens'},
  // PASTA & GRAINS
  {emoji:'🍝',name:'Spaghetti Carbonara',cal:620,prot:28,carb:72,fat:26,tag:'pasta',ingredients:'200g spaghetti, 100g pancetta or guanciale, 3 eggs + 2 yolks, 80g pecorino romano, black pepper, salt, pasta water'},
  {emoji:'🍝',name:'Pesto Pasta',cal:550,prot:18,carb:68,fat:22,tag:'pasta',ingredients:'200g pasta, 3 tbsp basil pesto, 100g cherry tomatoes, 30g pine nuts, parmesan, fresh basil, olive oil, salt, lemon'},
  {emoji:'🫕',name:'Risotto ai Funghi',cal:520,prot:16,carb:72,fat:18,tag:'pasta',ingredients:'300g arborio rice, 300g mixed mushrooms, onion, garlic, white wine, 1 litre vegetable stock, butter, parmesan, thyme, truffle oil'},
  {emoji:'🍝',name:'Arrabiata',cal:480,prot:14,carb:74,fat:14,tag:'pasta',ingredients:'200g penne, 1 can crushed tomatoes, 3 garlic cloves, 2 tsp chili flakes, 3 tbsp olive oil, fresh parsley, parmesan, salt'},
  {emoji:'🌾',name:'Tabbouleh',cal:280,prot:8,carb:42,fat:10,tag:'pasta',ingredients:'100g bulgur wheat, 2 cups fresh parsley, mint, cherry tomatoes, cucumber, spring onion, lemon juice, olive oil, salt, pepper'},
  // SWEET & SNACKS
  {emoji:'🍌',name:'Banana Protein Bites',cal:180,prot:10,carb:24,fat:6,tag:'snack',ingredients:'2 bananas, 80g rolled oats, 1 scoop protein powder, 2 tbsp peanut butter, 1 tbsp honey, dark chocolate chips'},
  {emoji:'🍫',name:'Energy Balls',cal:160,prot:6,carb:20,fat:8,tag:'snack',ingredients:'100g rolled oats, 4 tbsp peanut butter, 2 tbsp honey, 2 tbsp dark chocolate chips, 1 tbsp chia seeds, 1 tsp vanilla'},
  {emoji:'🧁',name:'Protein Muffins',cal:210,prot:14,carb:26,fat:6,tag:'snack',ingredients:'2 scoops protein powder, 2 bananas, 2 eggs, 80g oat flour, 1 tsp baking powder, 1 tsp vanilla, blueberries, pinch salt'},
  {emoji:'🍎',name:'Apple & Nut Butter',cal:220,prot:6,carb:32,fat:10,tag:'snack',ingredients:'1 large apple (sliced), 2 tbsp almond butter, 1 tbsp granola, pinch cinnamon, drizzle honey'},
  {emoji:'🧀',name:'Cheese & Crackers Board',cal:350,prot:16,carb:28,fat:20,tag:'snack',ingredients:'60g aged cheddar, 60g brie, 6 wholegrain crackers, grapes, apple slices, walnuts, honey, fig jam'},
  // CHICKEN
  {emoji:'🍗',name:'Chicken Tikka Masala',cal:560,prot:42,carb:40,fat:22,tag:'chicken',ingredients:'300g chicken breast, tikka paste, 1 can crushed tomatoes, 100ml cream, onion, garlic, ginger, garam masala, coriander, basmati rice'},
  {emoji:'🐔',name:'Honey Garlic Chicken',cal:490,prot:40,carb:34,fat:18,tag:'chicken',ingredients:'4 chicken thighs, 3 tbsp honey, 4 garlic cloves, soy sauce, 1 tbsp apple cider vinegar, olive oil, rosemary, mashed potato'},
  {emoji:'🍗',name:'Chicken Caesar Salad',cal:420,prot:38,carb:18,fat:22,tag:'chicken',ingredients:'200g grilled chicken, romaine lettuce, caesar dressing, parmesan, croutons, anchovies, lemon juice, black pepper'},
  {emoji:'🫕',name:'One-Pan Chicken & Veg',cal:480,prot:42,carb:28,fat:20,tag:'chicken',ingredients:'4 chicken thighs, 2 sweet potatoes, broccoli, red onion, olive oil, paprika, garlic powder, oregano, salt, pepper, lemon'},
  {emoji:'🌯',name:'Chicken Burrito Bowl',cal:550,prot:44,carb:54,fat:16,tag:'chicken',ingredients:'200g chicken breast, 150g rice, black beans, corn, salsa, sour cream, guacamole, cheddar, lime juice, cumin, chili'},
  // BEEF & PORK
  {emoji:'🍔',name:'Lean Beef Burger',cal:580,prot:40,carb:44,fat:24,tag:'beef',ingredients:'200g lean beef mince, burger bun, lettuce, tomato, red onion, pickles, cheddar, mustard, mayo, salt, pepper, smoked paprika'},
  {emoji:'🥩',name:'Beef Tacos',cal:500,prot:34,carb:48,fat:18,tag:'beef',ingredients:'200g beef mince, taco shells, salsa, sour cream, cheddar, lettuce, tomato, avocado, lime, cumin, chili powder, garlic'},
  {emoji:'🍖',name:'Slow-Cooked Pulled Pork',cal:560,prot:42,carb:38,fat:24,tag:'beef',ingredients:'400g pork shoulder, BBQ sauce, apple cider vinegar, brown sugar, paprika, garlic powder, onion powder, coleslaw, buns'},
  {emoji:'🥘',name:'Beef Bolognese',cal:580,prot:36,carb:62,fat:22,tag:'beef',ingredients:'250g beef mince, 200g spaghetti, 1 can crushed tomatoes, onion, carrot, celery, garlic, red wine, olive oil, basil, parmesan'},
  // PLANT-BASED
  {emoji:'🌱',name:'Tofu Scramble',cal:300,prot:20,carb:16,fat:16,tag:'plant-based',ingredients:'400g firm tofu (crumbled), turmeric, nutritional yeast, soy sauce, onion, bell pepper, spinach, garlic, olive oil, toast'},
  {emoji:'🥜',name:'Peanut Noodles',cal:520,prot:18,carb:68,fat:20,tag:'plant-based',ingredients:'200g noodles, 3 tbsp peanut butter, 2 tbsp soy sauce, 1 tbsp sesame oil, lime juice, garlic, ginger, chili, cucumber, carrot, coriander'},
  {emoji:'🌿',name:'Stuffed Bell Peppers',cal:380,prot:14,carb:52,fat:12,tag:'plant-based',ingredients:'3 bell peppers, 150g quinoa, 1 can black beans, corn, tomatoes, cumin, chili, coriander, lime, cheddar (optional)'},
  {emoji:'🍄',name:'Mushroom Stroganoff',cal:440,prot:14,carb:56,fat:18,tag:'plant-based',ingredients:'400g mixed mushrooms, 1 onion, garlic, 200ml plant cream, Dijon mustard, paprika, thyme, vegetable stock, tagliatelle, parsley'},
  {emoji:'🥑',name:'Vegan Buddha Bowl',cal:460,prot:16,carb:60,fat:18,tag:'plant-based',ingredients:'150g roasted chickpeas, 100g quinoa, sweet potato, kale, avocado, tahini dressing, hemp seeds, edamame, cherry tomatoes'},
];

// ─── LOAD / SAVE ─────────────────────────────────────────────────────────────
function loadStorage(){
  try{
    const g=localStorage.getItem('nourish_goals');
    if(g)goals=JSON.parse(g);
    const d=localStorage.getItem('nourish_days');
    if(d)allDays=JSON.parse(d);
  }catch(e){}
}
function saveStorage(){
  try{
    localStorage.setItem('nourish_goals',JSON.stringify(goals));
    localStorage.setItem('nourish_days',JSON.stringify(allDays));
  }catch(e){}
}
function getDayKey(){return dayOffset.toString()}
function getCurrentMeals(){
  const k=getDayKey();
  if(!allDays[k])allDays[k]={breakfast:[],lunch:[],dinner:[],snacks:[]};
  return allDays[k];
}
function saveDay(){
  allDays[getDayKey()]={...getCurrentMeals()};
  saveStorage();
}

// ─── STATS ───────────────────────────────────────────────────────────────────
function getTotals(mealsObj){
  const all=[...mealsObj.breakfast,...mealsObj.lunch,...mealsObj.dinner,...mealsObj.snacks];
  return{
    cal:all.reduce((s,f)=>s+f.cal,0),
    prot:all.reduce((s,f)=>s+f.prot,0),
    carb:all.reduce((s,f)=>s+f.carb,0),
    fat:all.reduce((s,f)=>s+(f.fat||0),0)
  };
}
function updateStats(){
  const m=getCurrentMeals();
  const tot=getTotals(m);
  document.getElementById('totalCal').textContent=tot.cal;
  document.getElementById('totalProt').textContent=tot.prot;
  document.getElementById('totalCarb').textContent=tot.carb;
  document.getElementById('calLeft').textContent=Math.max(0,goals.cal-tot.cal);
  document.getElementById('protGoalShow').textContent=goals.prot;
  document.getElementById('carbGoalShow').textContent=goals.carb;
  const pct=(v,g)=>Math.min(100,Math.round(v/g*100));
  document.getElementById('calBar').style.width=pct(tot.cal,goals.cal)+'%';
  document.getElementById('protBar').style.width=pct(tot.prot,goals.prot)+'%';
  document.getElementById('carbBar').style.width=pct(tot.carb,goals.carb)+'%';
  document.getElementById('calBar').className='progress-fill '+(tot.cal>goals.cal?'over':'cal-fill');
}

// ─── WEEK GRID ───────────────────────────────────────────────────────────────
const dayNames=['sun','mon','tue','wed','thu','fri','sat'];
function renderWeek(){
  const grid=document.getElementById('weekGrid');
  grid.innerHTML='';
  const today=new Date();
  // Show current week (Mon-Sun)
  const dow=today.getDay();
  const mondayOffset=-(dow===0?6:dow-1);
  for(let i=0;i<7;i++){
    const d=new Date(today);
    d.setDate(today.getDate()+mondayOffset+i);
    const diff=Math.round((d-today)/(1000*60*60*24));
    const actualOffset=diff;
    const k=actualOffset.toString();
    const meals=allDays[k]||{breakfast:[],lunch:[],dinner:[],snacks:[]};
    const dayCal=getTotals(meals).cal;
    const el=document.createElement('div');
    el.className='week-day'+(actualOffset===0?' today':'')+(actualOffset===dayOffset?' selected':'');
    const dn=dayNames[d.getDay()];
    el.innerHTML=`<div class="wd-name">${t(dn)}</div><div class="wd-num">${d.getDate()}</div><div class="wd-cal">${dayCal>0?dayCal+'':'-'}</div>`;
    el.addEventListener('click',()=>{dayOffset=actualOffset;renderAll();});
    grid.appendChild(el);
  }
}

// ─── DATE LABEL ──────────────────────────────────────────────────────────────
function getDateLabel(){
  if(dayOffset===0)return t('today');
  const d=new Date();d.setDate(d.getDate()+dayOffset);
  const locales={'en':'en-GB','no':'nb-NO','es':'es-ES','fr':'fr-FR','de':'de-DE','it':'it-IT','pt':'pt-PT','zh':'zh-CN','ja':'ja-JP','ar':'ar-SA'};
  return d.toLocaleDateString(locales[lang]||'en-GB',{weekday:'long',month:'short',day:'numeric'});
}

// ─── MEALS ───────────────────────────────────────────────────────────────────
function renderMeals(){
  const wrap=document.getElementById('mealsWrap');
  wrap.innerHTML='';
  const meals=getCurrentMeals();
  mealKeys.forEach(mk=>{
    const foods=meals[mk];
    const meta=mealMeta[mk];
    const mCal=foods.reduce((s,f)=>s+f.cal,0);
    const mProt=foods.reduce((s,f)=>s+f.prot,0);
    const mCarb=foods.reduce((s,f)=>s+f.carb,0);
    const card=document.createElement('div');card.className='meal-card';
    const foodRows=foods.map((f,i)=>`
      <div class="food-row">
        <span class="food-name">${f.name}</span>
        <span class="food-num">${f.cal} kcal</span>
        <span class="food-prot">${f.prot}g P</span>
        <span class="food-num" style="color:#ffa726">${f.carb}g C</span>
        <button class="food-del" data-meal="${mk}" data-i="${i}">×</button>
      </div>`).join('');
    card.innerHTML=`
      <div class="meal-header" data-meal="${mk}">
        <div class="meal-left">
          <div class="meal-icon" style="background:${meta.bg}">${meta.icon}</div>
          <div>
            <div class="meal-name">${t(mk)}</div>
            <div class="meal-stats">${mCal} kcal · ${mProt}g P · ${mCarb}g C</div>
          </div>
        </div>
        <div class="meal-right">
          <div class="meal-kcal">${mCal}</div>
          <div class="chevron open" id="chev-${mk}">▾</div>
        </div>
      </div>
      <div class="meal-body open" id="body-${mk}">
        ${foods.length>0?`<div class="food-list">${foodRows}</div>`:''}
        <div class="add-section">
          <div class="add-grid">
            <input type="text" id="in-name-${mk}" placeholder="${t('addFood')}">
            <input type="number" id="in-cal-${mk}" placeholder="${t('kcal')}">
            <input type="number" id="in-prot-${mk}" placeholder="${t('prot')}">
            <input type="number" id="in-carb-${mk}" placeholder="${t('carb')}">
            <button class="add-btn" data-meal="${mk}">${t('addBtn')}</button>
          </div>
          <button class="ai-meal-btn" data-meal="${mk}">
            <span class="ai-spark">✦</span> ${t('aiSuggest')}
          </button>
          <div class="ai-box" id="ai-${mk}"></div>
        </div>
      </div>`;
    wrap.appendChild(card);
  });

  // Toggle open/close
  wrap.querySelectorAll('.meal-header').forEach(h=>{
    h.addEventListener('click',e=>{
      if(e.target.closest('.food-del'))return;
      const mk=h.dataset.meal;
      const body=document.getElementById('body-'+mk);
      const chev=document.getElementById('chev-'+mk);
      body.classList.toggle('open');
      chev.classList.toggle('open');
    });
  });

  // Delete food
  wrap.querySelectorAll('.food-del').forEach(btn=>{
    btn.addEventListener('click',e=>{
      e.stopPropagation();
      const mk=btn.dataset.meal,i=parseInt(btn.dataset.i);
      getCurrentMeals()[mk].splice(i,1);
      saveDay();renderMeals();updateStats();renderWeek();
    });
  });

  // Add food
  wrap.querySelectorAll('.add-btn[data-meal]').forEach(btn=>{
    btn.addEventListener('click',()=>addFood(btn.dataset.meal));
  });

  // Enter key
  mealKeys.forEach(mk=>{
    ['in-name-','in-cal-','in-prot-','in-carb-'].forEach(p=>{
      const el=document.getElementById(p+mk);
      if(el)el.addEventListener('keydown',e=>{if(e.key==='Enter')addFood(mk);});
    });
  });

  // AI suggest
  wrap.querySelectorAll('.ai-meal-btn').forEach(btn=>{
    btn.addEventListener('click',()=>aiSuggest(btn.dataset.meal));
  });
}

function addFood(mk){
  const name=document.getElementById('in-name-'+mk).value.trim();
  if(!name)return;
  const cal=parseInt(document.getElementById('in-cal-'+mk).value)||0;
  const prot=parseInt(document.getElementById('in-prot-'+mk).value)||0;
  const carb=parseInt(document.getElementById('in-carb-'+mk).value)||0;
  getCurrentMeals()[mk].push({name,cal,prot,carb,fat:0});
  saveDay();renderMeals();updateStats();renderWeek();
}

async function aiSuggest(mk){
  const box=document.getElementById('ai-'+mk);
  box.className='ai-box show';
  box.innerHTML=`<span class="dots">${t('loading')}</span>`;
  const tot=getTotals(getCurrentMeals());
  try{
    const r=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1000,messages:[{role:'user',content:`You are a nutrition assistant. Suggest ONE healthy meal idea for ${t(mk)} (${mk}). The user has consumed today: ${tot.cal} kcal, ${tot.prot}g protein, ${tot.carb}g carbs. Their daily goals: ${goals.cal} kcal, ${goals.prot}g protein. Respond in language: "${lang}". Give the meal name, approximate calories, protein, and carbs, and 2-3 sentences about why it's a good choice. Be concise and encouraging.`}]})});
    const d=await r.json();
    box.textContent=d.content.map(c=>c.text||'').join('');
  }catch(e){box.textContent='(AI offline – check connection)';}
}

// ─── RECIPES ─────────────────────────────────────────────────────────────────
function renderRecipes(){
  document.getElementById('recipeTitle').textContent=t('recipes');
  const grid=document.getElementById('recipeGrid');
  grid.innerHTML='';
  const filterVal=(document.getElementById('recipeFilter')||{}).value||'all';
  const searchVal=((document.getElementById('recipeSearch')||{}).value||'').toLowerCase().trim();
  const filtered=recipes.map((r,idx)=>({r,idx})).filter(({r})=>{
    const matchTag=filterVal==='all'||r.tag===filterVal;
    const matchSearch=!searchVal||r.name.toLowerCase().includes(searchVal)||r.tag.includes(searchVal)||r.ingredients.toLowerCase().includes(searchVal);
    return matchTag&&matchSearch;
  });
  const countEl=document.getElementById('recipeCount');
  if(countEl)countEl.textContent=filtered.length+' recipes';
  filtered.forEach(({r,idx})=>{
    const c=document.createElement('div');c.className='recipe-card';
    c.innerHTML=`<div class="recipe-emoji">${r.emoji}</div>
      <div class="recipe-name">${r.name}</div>
      <div class="recipe-macro">${r.cal} kcal · ${r.prot}g P · ${r.carb}g C</div>
      <div class="recipe-tag">${r.tag}</div>`;
    c.addEventListener('click',()=>openRecipe(idx));
    grid.appendChild(c);
  });
}
function initRecipeFilters(){
  const s=document.getElementById('recipeSearch');
  const f=document.getElementById('recipeFilter');
  if(s)s.addEventListener('input',renderRecipes);
  if(f)f.addEventListener('change',renderRecipes);
}

async function openRecipe(idx){
  currentRecipeIdx=idx;
  const r=recipes[idx];
  document.getElementById('mTitle').textContent=r.emoji+' '+r.name;
  document.getElementById('mMacros').innerHTML=
    `<span class="macro-pill">🔥 ${r.cal} kcal</span>
     <span class="macro-pill">💪 ${r.prot}g P</span>
     <span class="macro-pill">🌾 ${r.carb}g C</span>
     <span class="macro-pill">🥑 ${r.fat}g F</span>`;
  document.getElementById('mIngredients').textContent=r.ingredients;
  const steps=document.getElementById('mSteps');
  steps.innerHTML=`<span class="dots">${t('loading')}</span>`;
  // Populate meal select
  const sel=document.getElementById('mMealSelect');
  sel.innerHTML=mealKeys.map(mk=>`<option value="${mk}">${t(mk)}</option>`).join('');
  document.getElementById('recipeModal').classList.add('open');
  try{
    const resp=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1000,messages:[{role:'user',content:`Write a clear, concise step-by-step recipe for "${r.name}" using: ${r.ingredients}. Respond in language: "${lang}". Use numbered steps (1. 2. 3. etc). Keep to 4-6 steps. Be practical and easy to follow.`}]})});
    const d=await resp.json();
    steps.textContent=d.content.map(c=>c.text||'').join('');
  }catch(e){steps.textContent='(AI offline)';}
}

document.getElementById('mClose').addEventListener('click',()=>document.getElementById('recipeModal').classList.remove('open'));
document.getElementById('recipeModal').addEventListener('click',e=>{if(e.target===document.getElementById('recipeModal'))document.getElementById('recipeModal').classList.remove('open');});
document.getElementById('mUseBtn').addEventListener('click',()=>{
  if(currentRecipeIdx===null)return;
  const r=recipes[currentRecipeIdx];
  const mk=document.getElementById('mMealSelect').value;
  getCurrentMeals()[mk].push({name:r.name,cal:r.cal,prot:r.prot,carb:r.carb,fat:r.fat});
  saveDay();renderMeals();updateStats();renderWeek();
  document.getElementById('recipeModal').classList.remove('open');
  switchTab('planner');
});

// ─── GOALS ───────────────────────────────────────────────────────────────────
function loadGoalInputs(){
  document.getElementById('gCal').value=goals.cal;
  document.getElementById('gProt').value=goals.prot;
  document.getElementById('gCarb').value=goals.carb;
  document.getElementById('gFat').value=goals.fat;
}
document.getElementById('saveGoalsBtn').addEventListener('click',()=>{
  goals={
    cal:parseInt(document.getElementById('gCal').value)||2000,
    prot:parseInt(document.getElementById('gProt').value)||150,
    carb:parseInt(document.getElementById('gCarb').value)||250,
    fat:parseInt(document.getElementById('gFat').value)||65
  };
  saveStorage();updateStats();
  const btn=document.getElementById('saveGoalsBtn');
  btn.textContent='✓ Saved!';
  setTimeout(()=>btn.textContent=t('saveGoals'),1500);
});

// ─── TABS ────────────────────────────────────────────────────────────────────
function switchTab(tab){
  document.querySelectorAll('.nav-tab,.mobile-tab').forEach(b=>b.classList.remove('active'));
  document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
  document.getElementById('view-'+tab).classList.add('active');
  document.querySelectorAll('[data-tab="'+tab+'"]').forEach(b=>b.classList.add('active'));
}
document.querySelectorAll('.nav-tab,.mobile-tab').forEach(btn=>{
  btn.addEventListener('click',()=>switchTab(btn.dataset.tab));
});

// ─── LANGUAGE ────────────────────────────────────────────────────────────────
function applyLang(){
  document.querySelectorAll('[data-i18n]').forEach(el=>{el.textContent=t(el.dataset.i18n);});
  document.getElementById('mtPlanner').textContent=t('planner');
  document.getElementById('mtRecipes').textContent=t('recipes');
  document.getElementById('mtGoals').textContent=t('goals');
}
document.getElementById('langSelect').addEventListener('change',e=>{
  lang=e.target.value;
  applyLang();renderAll();
});

// ─── DATE NAV ────────────────────────────────────────────────────────────────
document.getElementById('prevDay').addEventListener('click',()=>{dayOffset--;renderAll();});
document.getElementById('nextDay').addEventListener('click',()=>{dayOffset++;renderAll();});

// ─── FULL RENDER ─────────────────────────────────────────────────────────────
function renderAll(){
  document.getElementById('dateLabel').textContent=getDateLabel();
  renderWeek();
  renderMeals();
  renderRecipes();
  updateStats();
  applyLang();
  loadGoalInputs();
}

// ─── INIT ────────────────────────────────────────────────────────────────────
loadStorage();
renderAll();
initRecipeFilters();
</script>
</body>
</html>

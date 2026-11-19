<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Чек-лист Хаб — Каталог, Чек-листы, Форум и Профиль</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

    :root {
      color-scheme: dark;
      --bg: #0c0d10;
      --bg-elevated: #14161c;
      --bg-card: #191c24;
      --accent: #e11d48;
      --accent-2: #f59e0b;
      --ok: #10b981;
    }

    body {
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
      background-color: #0c0d10;
      color: #f3f4f6;
      min-height: 100vh;
    }

    .check-row.is-done .check-text {
      text-decoration: line-through;
      color: #9ca3af;
    }

    .group-body.is-collapsed {
      display: none;
    }

    .chev.is-collapsed {
      transform: rotate(-90deg);
    }
  </style>
</head>
<body class="antialiased selection:bg-[#e11d48]/30 selection:text-rose-200">
  <!-- Верхняя панель навигации: Каталог, Форум, Профиль/Вход и Бэкапы -->
  <header class="sticky top-0 z-30 border-b border-white/10 bg-[#0c0d10]/90 backdrop-blur-md">
    <div class="mx-auto flex max-w-6xl flex-wrap items-center justify-between gap-3 px-4 py-3">
      <div class="flex flex-wrap items-center gap-4">
        <button
          id="homeBrandBtn"
          type="button"
          class="flex items-center gap-3 rounded-xl text-left transition hover:opacity-90"
        >
          <div class="flex h-10 w-10 shrink-0 items-center justify-center rounded-xl bg-gradient-to-br from-[#e11d48] to-[#f59e0b] text-sm font-extrabold text-white shadow-lg shadow-rose-950/60">
            ЧХ
          </div>
          <div>
            <div class="text-base font-bold leading-tight text-white">Чек-лист Хаб</div>
            <div class="text-xs text-gray-400">Трекер, форум и профиль игрока</div>
          </div>
        </button>

        <nav class="flex items-center gap-1.5 rounded-xl border border-white/10 bg-[#14161c] p-1">
          <button
            id="navCatalogBtn"
            type="button"
            class="rounded-lg px-3 py-1.5 text-xs font-semibold transition"
          >
            Каталог
          </button>
          <button
            id="navForumBtn"
            type="button"
            class="rounded-lg px-3 py-1.5 text-xs font-semibold transition"
          >
            Форум
          </button>
        </nav>
      </div>

      <div class="flex flex-wrap items-center gap-2">
        <button
          id="profileAuthPillBtn"
          type="button"
          class="flex items-center gap-2 rounded-full border border-white/10 bg-[#191c24] px-3 py-1.5 text-xs font-medium text-gray-200 transition hover:border-white/25 hover:bg-[#202430]"
          title="Открыть профиль или войти в аккаунт"
        >
          <span id="authStatusDot" class="h-2 w-2 rounded-full bg-amber-400"></span>
          <span id="authStatusLabel">Войти / Профиль</span>
        </button>

        <div
          id="storageStatusBadge"
          class="hidden items-center gap-2 rounded-full border border-white/10 bg-[#14161c] px-3 py-1.5 text-xs text-gray-400 sm:flex"
          title="Режим хранилища"
        >
          <span id="storageDot" class="h-2 w-2 rounded-full bg-[#10b981]"></span>
          <span id="storageText">Браузер</span>
        </div>

        <button
          id="exportJsonBtn"
          type="button"
          class="rounded-xl border border-white/10 bg-[#191c24] px-3 py-2 text-xs font-medium text-gray-200 transition hover:bg-[#222733]"
        >
          Экспорт JSON
        </button>

        <button
          id="importJsonBtn"
          type="button"
          class="rounded-xl border border-white/10 bg-[#191c24] px-3 py-2 text-xs font-medium text-gray-200 transition hover:bg-[#222733]"
        >
          Импорт JSON
        </button>
        <input id="importFileInput" type="file" accept="application/json" class="hidden" />
      </div>
    </div>
  </header>

  <!-- Основной контейнер экранов -->
  <main id="appRoot" class="mx-auto max-w-6xl px-4 py-6 pb-20"></main>

  <!-- Модальное окно создания своего чек-листа -->
  <div
    id="createModal"
    class="fixed inset-0 z-50 hidden items-center justify-center bg-black/75 p-4 backdrop-blur-sm"
    role="dialog"
    aria-modal="true"
    aria-labelledby="createModalTitle"
  >
    <div class="max-h-[90vh] w-full max-w-lg overflow-y-auto rounded-2xl border border-white/15 bg-[#14161c] p-5 shadow-2xl">
      <div class="mb-4 flex items-center justify-between gap-2">
        <h2 id="createModalTitle" class="text-lg font-bold text-white">Создать свой чек-лист</h2>
        <button
          id="closeCreateModalBtn"
          type="button"
          class="rounded-lg border border-white/10 bg-[#191c24] px-2.5 py-1 text-xs text-gray-400 hover:bg-white/10 hover:text-white"
        >
          ✕
        </button>
      </div>

      <form id="createChecklistForm" class="space-y-3">
        <div>
          <label for="customTitleInput" class="mb-1 block text-xs font-medium text-gray-300">Название</label>
          <input
            id="customTitleInput"
            type="text"
            required
            placeholder="Например: Elden Ring — Боссы или мой список"
            class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2.5 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none"
          />
        </div>

        <div class="grid grid-cols-1 gap-3 sm:grid-cols-2">
          <div>
            <label for="customCategoryInput" class="mb-1 block text-xs font-medium text-gray-300">Категория</label>
            <input
              id="customCategoryInput"
              type="text"
              value="Свой список"
              class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2.5 text-sm text-white focus:border-[#e11d48] focus:outline-none"
            />
          </div>
          <div>
            <label for="customGroupInput" class="mb-1 block text-xs font-medium text-gray-300">Название группы</label>
            <input
              id="customGroupInput"
              type="text"
              value="Основной список"
              class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2.5 text-sm text-white focus:border-[#e11d48] focus:outline-none"
            />
          </div>
        </div>

        <div>
          <label for="customItemsTextarea" class="mb-1 block text-xs font-medium text-gray-300">
            Пункты (каждый с новой строки)
          </label>
          <textarea
            id="customItemsTextarea"
            rows="6"
            required
            placeholder="Пункт 1&#10;Пункт 2&#10;Пункт 3"
            class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2.5 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none"
          ></textarea>
        </div>

        <div class="flex justify-end gap-2 pt-2">
          <button
            id="cancelCreateModalBtn"
            type="button"
            class="rounded-xl border border-white/10 bg-[#191c24] px-4 py-2 text-xs font-medium text-gray-300 hover:bg-white/10"
          >
            Отмена
          </button>
          <button
            type="submit"
            class="rounded-xl bg-[#e11d48] px-4 py-2 text-xs font-semibold text-white transition hover:bg-rose-500"
          >
            Создать чек-лист
          </button>
        </div>
      </form>
    </div>
  </div>

  <!-- Модальное окно входа / регистрации / быстрого демо-профиля -->
  <div
    id="authModal"
    class="fixed inset-0 z-50 hidden items-center justify-center bg-black/75 p-4 backdrop-blur-sm"
    role="dialog"
    aria-modal="true"
    aria-labelledby="authModalTitle"
  >
    <div class="max-h-[92vh] w-full max-w-md overflow-y-auto rounded-2xl border border-white/15 bg-[#14161c] p-5 shadow-2xl">
      <div class="mb-4 flex items-center justify-between gap-2">
        <h2 id="authModalTitle" class="text-lg font-bold text-white">Аккаунт игрока</h2>
        <button
          id="closeAuthModalBtn"
          type="button"
          class="rounded-lg border border-white/10 bg-[#191c24] px-2.5 py-1 text-xs text-gray-400 hover:bg-white/10 hover:text-white"
        >
          ✕
        </button>
      </div>

      <!-- Переключатель Вход / Регистрация -->
      <div class="mb-4 grid grid-cols-2 gap-1.5 rounded-xl border border-white/10 bg-[#0c0d10] p-1">
        <button
          id="authTabLoginBtn"
          type="button"
          class="rounded-lg py-2 text-xs font-semibold transition"
        >
          Вход
        </button>
        <button
          id="authTabRegisterBtn"
          type="button"
          class="rounded-lg py-2 text-xs font-semibold transition"
        >
          Регистрация
        </button>
      </div>

      <div id="authErrorBox" class="mb-3 hidden rounded-xl border border-red-500/40 bg-red-500/15 px-3 py-2 text-xs text-red-200"></div>

      <!-- Форма входа -->
      <form id="loginForm" class="space-y-3">
        <div>
          <label for="loginIdentifierInput" class="mb-1 block text-xs font-medium text-gray-300">
            Никнейм или Email / @handle
          </label>
          <input
            id="loginIdentifierInput"
            type="text"
            required
            placeholder="Например: jin_sakai или jin@tsushima.gg"
            class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2.5 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none"
          />
        </div>

        <div>
          <label for="loginPasswordInput" class="mb-1 block text-xs font-medium text-gray-300">Пароль</label>
          <input
            id="loginPasswordInput"
            type="password"
            required
            placeholder="Введите пароль"
            class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2.5 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none"
          />
        </div>

        <button
          type="submit"
          class="w-full rounded-xl bg-[#e11d48] py-2.5 text-xs font-semibold text-white transition hover:bg-rose-500"
        >
          Войти в профиль
        </button>
      </form>

      <!-- Форма регистрации -->
      <form id="registerForm" class="hidden space-y-3">
        <div>
          <label for="regUsernameInput" class="mb-1 block text-xs font-medium text-gray-300">
            Никнейм (от 2 до 24 символов)
          </label>
          <input
            id="regUsernameInput"
            type="text"
            required
            placeholder="Например: ПризракЦусимы"
            class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2.5 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none"
          />
        </div>

        <div>
          <label for="regHandleInput" class="mb-1 block text-xs font-medium text-gray-300">
            Email или @handle
          </label>
          <input
            id="regHandleInput"
            type="text"
            required
            placeholder="player@example.com или @liberty_driver"
            class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2.5 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none"
          />
        </div>

        <div>
          <label for="regPasswordInput" class="mb-1 block text-xs font-medium text-gray-300">
            Пароль (минимум 4 символа)
          </label>
          <input
            id="regPasswordInput"
            type="password"
            required
            placeholder="Придумайте пароль"
            class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2.5 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none"
          />
        </div>

        <div>
          <label for="regBioInput" class="mb-1 block text-xs font-medium text-gray-300">О себе (необязательно)</label>
      <!-- Быстрый вход / регистрация через Google и демо-профиль -->
      <div class="mt-4 border-t border-white/10 pt-4">
        <div class="mb-2 text-[11px] font-medium text-gray-400">Быстрый вход без долгого заполнения форм:</div>
        <button
          id="googleQuickSignInBtn"
          type="button"
          class="mb-2 flex w-full items-center justify-center gap-2.5 rounded-xl border border-white/15 bg-white py-2.5 text-xs font-semibold text-gray-900 shadow-sm transition hover:bg-gray-100"
        >
          <svg class="h-4 w-4 shrink-0" viewBox="0 0 24 24" aria-hidden="true">
            <path fill="#4285F4" d="M23.49 12.27c0-.79-.07-1.54-.19-2.27H12v4.51h6.47c-.29 1.5-1.14 2.77-2.4 3.62v3.01h3.88c2.27-2.09 3.54-5.17 3.54-8.87z"/>
            <path fill="#34A853" d="M12 24c3.24 0 5.95-1.08 7.93-2.91l-3.88-3.01c-1.08.72-2.45 1.16-4.05 1.16-3.12 0-5.77-2.11-6.72-4.96H1.26v3.1C3.23 21.3 7.28 24 12 24z"/>
            <path fill="#FBBC05" d="M5.28 14.28c-.24-.72-.38-1.49-.38-2.28s.14-1.56.38-2.28V6.62H1.26C.46 8.21 0 10.05 0 12s.46 3.79 1.26 5.38l4.02-3.1z"/>
            <path fill="#EA4335" d="M12 4.75c1.77 0 3.35.61 4.6 1.8l3.42-3.42C17.95 1.19 15.24 0 12 0 7.28 0 3.23 2.7 1.26 6.62l4.02 3.1c.95-2.85 3.6-4.97 6.72-4.97z"/>
          </svg>
          <span>Продолжить с Google</span>
        </button>
        <button
          id="quickDemoLoginBtn"
          type="button"
          class="w-full rounded-xl border border-[#f59e0b]/30 bg-[#f59e0b]/10 py-2 text-xs font-semibold text-amber-200 transition hover:bg-[#f59e0b]/20"
        >
          Создать / войти в демо-профиль «Искатель 100%»
        </button>
        <p class="mt-2 text-[11px] leading-relaxed text-gray-500">
          В локальном режиме вход через Google создаёт готовый профиль в браузере; при подключении облачной базы (Supabase/Firebase) сюда подключается реальный OAuth.
        </p>
      </div>
    </div>
  </div>

  <!-- Всплывающее уведомление -->
  <div
    id="toastBox"
    class="pointer-events-none fixed bottom-5 right-5 z-50 rounded-xl border border-white/15 bg-[#191c24] px-4 py-2.5 text-xs font-medium text-white opacity-0 shadow-xl transition duration-200"
    role="status"
    aria-live="polite"
  ></div>

  <script>
    (function () {
      const STORAGE_KEY = "checklist_hub_forum_profile_v1";
      const memoryStore = new Map();
      let storageBackend = "localStorage";
      let pendingResetConfirm = false;
      let resetTimer = null;

      // Состояние фильтров и навигации
      let checklistSearch = "";
      let checklistFilter = "all"; // all | todo | done
      let forumCategory = "Все";
      let forumSearch = "";
      let forumSort = "new"; // new | active
      let authModalMode = "login"; // login | register

      function readStorage() {
        try {
          if (window.localStorage) {
            const raw = window.localStorage.getItem(STORAGE_KEY);
            storageBackend = "localStorage";
            return raw;
          }
        } catch (err) {
          // Откат в память при ограничении localStorage
        }
        storageBackend = "memory";
        return memoryStore.get(STORAGE_KEY) || null;
      }

      function writeStorage(raw) {
        try {
          if (window.localStorage) {
            window.localStorage.setItem(STORAGE_KEY, raw);
            storageBackend = "localStorage";
            return true;
          }
        } catch (err) {
          // Сохраняем в память сессии
        }
        storageBackend = "memory";
        memoryStore.set(STORAGE_KEY, raw);
        return false;
      }

      function syncStorageIndicator() {
        const dot = document.getElementById("storageDot");
        const text = document.getElementById("storageText");
        if (!dot || !text) return;
        if (storageBackend === "localStorage") {
          dot.className = "h-2 w-2 rounded-full bg-[#10b981]";
          text.textContent = "Браузер";
        } else {
          dot.className = "h-2 w-2 rounded-full bg-[#f59e0b]";
          text.textContent = "Сессия";
        }
      }

      function showToast(msg) {
        const box = document.getElementById("toastBox");
        if (!box) return;
        box.textContent = msg;
        box.classList.remove("opacity-0");
        box.classList.add("opacity-100");
        clearTimeout(showToast._timer);
        showToast._timer = setTimeout(() => {
          box.classList.remove("opacity-100");
          box.classList.add("opacity-0");
        }, 2400);
      }

      function numbered(prefix, count) {
        return Array.from({ length: count }, (_, i) => `${prefix} №${i + 1}`);
      }

      function escapeHtml(value) {
        return String(value ?? "")
          .replace(/&/g, "&amp;")
          .replace(/</g, "&lt;")
          .replace(/>/g, "&gt;")
          .replace(/"/g, "&quot;");
      }

      function getInitials(name) {
        const clean = String(name || "ИГ").trim();
        if (!clean) return "ИГ";
        const parts = clean.split(/\s+/);
        if (parts.length >= 2) {
          return (parts[0][0] + parts[1][0]).toUpperCase();
        }
        return clean.slice(0, 2).toUpperCase();
      }

      function formatDateRu(isoOrStr) {
        const d = new Date(isoOrStr);
        if (Number.isNaN(d.getTime())) return String(isoOrStr || "Сегодня");
        return d.toLocaleDateString("ru-RU", {
          day: "2-digit",
          month: "short",
          year: "numeric"
        });
      }

      // Полный чек-лист Ghost of Tsushima
      const GHOST_OF_TSUSHIMA = {
        id: "ghost-of-tsushima",
        title: "Ghost of Tsushima (Призрак Цусимы)",
        subtitle: "Пролог, Акты 1–3: сюжет, персонажи, побочные и легендарные истории, коллекционки, освобождение и трофеи",
        badge: "100% + Платина",
        category: "Action / Adventure",
        tabs: [
          {
            id: "got-prologue-act1",
            title: "Пролог и Акт 1: Идзухара",
            acts: [
              {
                id: "got-prologue",
                title: "Пролог",
                subtitle: "Вступление",
                groups: [
                  { id: "got-pro-story", title: "Сюжет", items: ["Пролог"] }
                ]
              },
              {
                id: "got-act1",
                title: "Акт 1. Идзухара",
                subtitle: "Южный регион острова Цусима",
                groups: [
                  {
                    id: "got-a1-story",
                    title: "1. Сюжетные задания",
                    items: [
                      "Кодекс воина",
                      "История сэнсэя Исикавы",
                      "История госпожи Масако",
                      "Сломленный кузнец",
                      "Молот и горн",
                      "Кровь на траве",
                      "История Рюдзо",
                      "Железный крюк",
                      "Тень самурая",
                      "Новый горизонт"
                    ]
                  },
                  {
                    id: "got-a1-ishikawa",
                    title: "2. Персонажи — Сэнсэй Исикава",
                    items: [
                      "История сэнсэя Исикавы",
                      "Сэнсэй и ученик",
                      "Оковы прошлого",
                      "Путь лучника"
                    ]
                  },
                  {
                    id: "got-a1-masako",
                    title: "2. Персонажи — Госпожа Масако",
                    items: [
                      "История госпожи Масако",
                      "Главарь",
                      "Супруг",
                      "Предатель",
                      "Материнский покой"
                    ]
                  },
                  {
                    id: "got-a1-kenji-ryuzo",
                    title: "2. Персонажи — Кэндзи и Рюдзо",
                    items: [
                      "Кэндзи: Слуга народа",
                      "Рюдзо: История Рюдзо"
                    ]
                  },
                  {
                    id: "got-a1-side",
                    title: "3. Дополнительные задания",
                    items: [
                      "Источники Хиёси",
                      "Зов родного дома",
                      "Цена железа",
                      "За Цусиму",
                      "Цена сакэ",
                      "Шёпот в лесах",
                      "По ту сторону чести",
                      "Во имя чести",
                      "Незаконченное дело",
                      "Погребённая честь",
                      "Рука целителя",
                      "Пустые корзины",
                      "Потерянные в море",
                      "Смеющиеся разбойники",
                      "История главы деревни",
                      "Сжечь стоянку лесорубов",
                      "Происшествие на перевале Хиёси"
                    ]
                  },
                  {
                    id: "got-a1-mythic",
                    title: "4. Легендарные истории",
                    items: [
                      "Небесный удар",
                      "Легенда о Тадаёри",
                      "Проклятие Утицунэ"
                    ]
                  },
                  {
                    id: "got-a1-springs",
                    title: "5. Горячие источники (9/9)",
                    items: [
                      "1. Горячий источник резной горы",
                      "2. Горячий источник у дозорной башни замка",
                      "3. Горячий источник холма светлячков",
                      "4. Горячий источник золотого листа",
                      "5. Горячий источник гостиницы Хиёси",
                      "6. Горячий источник горного вида",
                      "7. Горячий источник тихой лощины",
                      "8. Горячий источник восходящих деревьев",
                      "9. Горячий источник морского берега"
                    ]
                  },
                  {
                    id: "got-a1-bamboo",
                    title: "5. Бамбуковые стойки (7/7)",
                    items: [
                      "1. Бамбуковая стойка Ариакэ",
                      "2. Бамбуковая стойка Адзамо",
                      "3. Бамбуковая стойка Хиёси",
                      "4. Бамбуковая стойка Касинэ",
                      "5. Бамбуковая стойка Комацу",
                      "6. Бамбуковая стойка Комода",
                      "7. Бамбуковая стойка Цуцу"
                    ]
                  },
                  {
                    id: "got-a1-shrines",
                    title: "5. Синтоистские святилища (7/7)",
                    items: [
                      "1. Святилище Наконечника стрелы",
                      "2. Святилище Подветренной горы",
                      "3. Святилище Сливовых цветов",
                      "4. Святилище Солнечной вершины",
                      "5. Святилище Целебной скалы",
                      "6. Святилище Весенних водопадов",
                      "7. Святилище Каменного дракона"
                    ]
                  },
                  {
                    id: "got-a1-fox",
                    title: "5. Лисьи норы (22/22)",
                    items: numbered("Лисья нора", 22)
                  },
                  {
                    id: "got-a1-haiku",
                    title: "5. Хокку (8 + 1 сюжетное)",
                    items: [
                      "1. Хокку Цуцу",
                      "2. Хокку Адзамо",
                      "3. Хокку Комацу",
                      "4. Хокку Касинэ",
                      "5. Хокку Ариакэ",
                      "6. Хокку Комода",
                      "7. Хокку Хиёси",
                      "8. Хокку Источников Хиёси",
                      "Сюжетное: Хокку о потере"
                    ]
                  },
                  {
                    id: "got-a1-artifacts",
                    title: "5. Монгольские артефакты (17/17)",
                    items: [
                      "1. Ааруул", "2. Дерево адак", "3. Собака банхар", "4. Пушка с чёрным порохом",
                      "5. Чаша", "6. Кинжал", "7. Египетская маска", "8. Золотой браслет",
                      "9. Подвесной кувшин", "10. Можжевельник", "11. Монгольские планы", "12. Монгольская лошадь",
                      "13. Пайцза", "14. Седло", "15. Уртуу", "16. Боевой рог", "17. Ятга"
                    ]
                  },
                  {
                    id: "got-a1-records",
                    title: "5. Записи (16/16)",
                    items: [
                      "1. Разговоры с ханом №1", "2. Разговоры с ханом №2", "3. Разговоры с ханом №3",
                      "4. Разговоры с ханом №4", "5. Разговоры с ханом №5", "6. Доставить Сэнсэю Исикаве",
                      "7. Первая встреча", "8. Встретьте нас в бухте Умуги", "9. Записки о музыке",
                      "10. Навыки для торговли", "11. Украденные воспоминания", "12. Чёрные пески",
                      "13. Гендзо в кузне Комацу", "14. Моей любви", "15. Наблюдения в Источниках Хиёси",
                      "16. Что произошло в Комоде"
                    ]
                  },
                  {
                    id: "got-a1-crickets",
                    title: "5. Поющие сверчки (10/10)",
                    items: numbered("Сверчок", 10)
                  },
                  {
                    id: "got-a1-banners",
                    title: "5. Знамёна сасимоно (28/28)",
                    items: numbered("Знамя", 28)
                  },
                  {
                    id: "got-a1-lighthouses",
                    title: "5. Маяки (3/3)",
                    items: ["Маяк Ариакэ", "Маяк Комода", "Маяк Цуцу"]
                  },
                  {
                    id: "got-a1-pillars",
                    title: "5. Столпы чести (7/7)",
                    items: [
                      "Столп чести №1 — набор меча «Секрет Фудзина»",
                      "Столп чести №2 — набор меча «Тьма Гэмбу»",
                      "Столп чести №3 — набор меча «Яд мамуси»",
                      "Столп чести №4 — набор меча «Бамбук весны»",
                      "Столп чести №5 — набор меча «Сумеречный они»",
                      "Столп чести №6 — набор меча «Кисть воина»",
                      "Столп чести №7 — набор меча «Угли Яси»"
                    ]
                  },
                  {
                    id: "got-a1-vanity",
                    title: "5. Предметы внешнего вида (7)",
                    items: [
                      "Повязка страха", "Повязка пламени", "Повязка мастера меча",
                      "Повязка павшего воина", "Соломенная шляпа Тэнгу", "Шляпа крестьянина", "Шляпа беженца"
                    ]
                  },
                  {
                    id: "got-a1-liberation",
                    title: "6. Освобождение Идзухары (24/24)",
                    items: [
                      "1. Деревня Аой", "2. Прибрежный лагерь", "3. Рыбацкая деревня Охама", "4. Стоянка лесорубов",
                      "5. Спутанный перекресток", "6. Поместье солёного ветра", "7. Переправа каменной арки", "8. Переправа стремительных вод",
                      "9. Разорённый лагерь", "10. Кузня Комацу", "11. Бухта Адзамо", "12. Мост в Куте",
                      "13. Деревня Кута", "14. Перекрёсток Ёйти", "15. Трактир «Ночлег странника»", "16. Додзё Огава",
                      "17. Старый торговый пост", "18. Селение Ягата", "19. Рыбацкая деревня Кэти", "20. Поместье Такэсики",
                      "21. Деревня Фурута", "22. Разрушенная Верфь", "23. Источник у трактира в Хиёси", "24. Замок Канэда"
                    ]
                  }
                ]
              }
            ]
          },
          {
            id: "got-act2",
            title: "Акт 2: Тоётама",
            acts: [
              {
                id: "got-act2-main",
                title: "Акт 2. Тоётама",
                subtitle: "Центральный регион острова",
                groups: [
                  {
                    id: "got-a2-story",
                    title: "1. Сюжетные задания",
                    items: [
                      "Огненное послание", "Стены Ярикавы", "Трус Ярикавы", "Призрак из Ярикавы",
                      "Призраки прошлого", "Кровавая плата", "Судьба Цусимы", "Из тьмы"
                    ]
                  },
                  {
                    id: "got-a2-ishikawa-yuna",
                    title: "2. Персонажи — Исикава и Юна",
                    items: [
                      "Исикава: Мечты о завоеваниях", "Исикава: Призрак и демон-сэнсэй",
                      "Исикава: Ужас Оцуны", "Исикава: Покой",
                      "Юна: История Юны", "Юна: Безмолвная смерть",
                      "Юна: Чёрный волк", "Юна: Кровавое послание"
                    ]
                  },
                  {
                    id: "got-a2-kenji-norio",
                    title: "2. Персонажи — Кэндзи и Норио",
                    items: [
                      "Кэндзи: Натто и торговец сакэ", "Кэндзи: Тонкое искусство переговоров",
                      "Норио: Последний монах-воин", "Норио: Три действия, три иллюзии",
                      "Норио: Призраки в тумане", "Норио: Так рождается страдание",
                      "Норио: Кровавая сутра", "Норио: Причина страданий", "Норио: Конец страданий"
                    ]
                  },
                  {
                    id: "got-a2-masako-yuriko",
                    title: "2. Персонажи — Масако и Юрико",
                    items: [
                      "Масако: Глупец", "Масако: Семейный человек", "Масако: Вор", "Масако: Заговорщик",
                      "Юрико: Гордецы не выживают", "Юрико: Искусство видеть"
                    ]
                  },
                  {
                    id: "got-a2-side",
                    title: "3. Дополнительные задания",
                    items: [
                      "Последняя просьба", "Оплаченный долг", "Бремя воровства", "Дети реки",
                      "Богач не знает нужды", "Щедрость госпожи Сандзё", "Мир для божества",
                      "Плоть и камень", "Нежданный гость", "Родственные узы"
                    ]
                  },
                  {
                    id: "got-a2-mythic",
                    title: "4. Легендарные истории и поединки Кодзиро",
                    items: [
                      "Несокрушимый Госаку", "Шесть клинков Кодзиро", "Дух мщения Ярикавы",
                      "Поединок в топях", "Поединок среди паучьих лилий", "Поединок у водопада",
                      "Поединок у бурных волн", "Поединок под осенними листьями", "Поединок у зеркала священного света"
                    ]
                  },
                  {
                    id: "got-a2-springs",
                    title: "5. Горячие источники (6/6)",
                    items: [
                      "Горячий источник бамбукового леса", "Горячий источник тени клёна",
                      "Горячий источник болотного прилива", "Горячий источник вьюнка",
                      "Горячий источник мшистого отдыха", "Горячий источник Ёсинаки"
                    ]
                  },
                  {
                    id: "got-a2-bamboo",
                    title: "5. Бамбуковые стойки (6/6)",
                    items: [
                      "Бамбуковая стойка Акасима", "Бамбуковая стойка Кубара", "Бамбуковая стойка Куси",
                      "Бамбуковая стойка Оцуна", "Бамбуковая стойка Умуги", "Бамбуковая стойка Ярикава"
                    ]
                  },
                  {
                    id: "got-a2-shrines",
                    title: "5. Синтоистские святилища (6/6)",
                    items: [
                      "Святилище Облачного утёса", "Святилище Туманной скалы", "Святилище Пышной вершины",
                      "Святилище Болотной скалы", "Святилище Багровой скалы", "Святилище Черепашьей скалы"
                    ]
                  },
                  {
                    id: "got-a2-fox",
                    title: "5. Лисьи норы (17/17)",
                    items: numbered("Лисья нора", 17)
                  },
                  {
                    id: "got-a2-haiku",
                    title: "5. Хокку (7/7)",
                    items: [
                      "Хокку Акасима", "Хокку Кубара", "Хокку Куси", "Хокку Оцуна", "Хокку Умуги",
                      "Хокку «О наследии» (Призраки прошлого)", "Хокку «О мимолётности» (Гордецы не выживают)"
                    ]
                  },
                  {
                    id: "got-a2-artifacts",
                    title: "5. Монгольские артефакты (17/17)",
                    items: [
                      "Китайская ваза", "Составной лук", "Сушёное мясо", "Клетка орла", "Греческая ваза",
                      "Череп лошади", "Стойка для молока", "Монгольская бомба", "Гуталы", "Монгольская сабля",
                      "Монгольский щит", "Поднос для подношений", "Колчан", "Шагай", "Бубен шамана", "Тооно", "Цам"
                    ]
                  },
                  {
                    id: "got-a2-records",
                    title: "5. Записи (16/16)",
                    items: [
                      "Возвращайся домой", "Разговоры с ханом №6", "Разговоры с ханом №7", "Разговоры с ханом №8",
                      "Глухие уши", "Уроки исцеления", "Хоти и монахи-воины", "Необходимое для выживания",
                      "Изгнанники", "Нормирование в крепости Ярикава", "Воспоминание", "Доклад управляющему Удзимасе",
                      "Целители Акасима", "Обряд Нукабукуро", "Момидзи из деревни Акасима", "Моему брату"
                    ]
                  },
                  {
                    id: "got-a2-crickets",
                    title: "5. Поющие сверчки (7/7)",
                    items: numbered("Сверчок", 7)
                  },
                  {
                    id: "got-a2-banners",
                    title: "5. Знамёна сасимоно (26/26)",
                    items: numbered("Знамя", 26)
                  },
                  {
                    id: "got-a2-lighthouses",
                    title: "5. Маяки (2/2)",
                    items: ["Маяк Акасимы", "Маяк Кубары"]
                  },
                  {
                    id: "got-a2-pillars",
                    title: "5. Столпы чести (9/9)",
                    items: [
                      "Столп чести №1 — набор меча «Удача Бисамона»",
                      "Столп чести №2 — «Дыхание Хатимана»",
                      "Столп чести №3 — «Праздник поединков»",
                      "Столп чести №4 — «Река золотых карпов»",
                      "Столп чести №5 — «Хидзики на солнце»",
                      "Столп чести №6 — «Охота на медведя»",
                      "Столп чести №7 — «Коготь лунного медведя»",
                      "Столп чести №8 — «Вера воина»",
                      "Столп чести №9 — «Кожура юдзу»"
                    ]
                  },
                  {
                    id: "got-a2-vanity",
                    title: "5. Предметы внешнего вида (7/7)",
                    items: [
                      "Повязка второго сына", "Повязка Гёдзэна", "Повязка целителя",
                      "Повязка цветения сливы", "Соломенная шляпа речного русла",
                      "Соломенная шляпа Тоётамы", "Соломенная шляпа духа леса"
                    ]
                  },
                  {
                    id: "got-a2-territories",
                    title: "6. Монгольские территории Тоётамы (16/16)",
                    items: [
                      "Форпост: Форт Имаи", "Форпост: Деревня Кисибэ", "Форпост: Поселение Нумата",
                      "Лагерь Тёмной воды", "Лагерь на краю леса", "Переправа Шипящего ручья",
                      "Одинокая лесная поляна", "Постоялый двор «Моховый свет»", "Руины на склоне горы",
                      "Убежище повстанцев", "Прибрежная ферма", "Уединённый маяк",
                      "Смотровая площадка Каменного болота",
                      "Ферма Иидзима", "Ферма Косимидзу", "Ферма Окада"
                    ]
                  }
                ]
              }
            ]
          },
          {
            id: "got-act3",
            title: "Акт 3: Камиагата",
            acts: [
              {
                id: "got-act3-main",
                title: "Акт 3. Камиагата",
                subtitle: "Северный регион острова",
                groups: [
                  {
                    id: "got-a3-story",
                    title: "1. Сюжетные задания",
                    items: [
                      "Честь и пепел", "Волки у порога", "Надвигающаяся буря",
                      "Сердце Дзито", "Вечное голубое небо", "История господина Симуры"
                    ]
                  },
                  {
                    id: "got-a3-chars",
                    title: "2. Истории персонажей",
                    items: [
                      "Сэнсэй Исикава: Друзья в пути",
                      "Госпожа Масако: Преданная сестра",
                      "Норио: Хранитель Цусимы",
                      "Норио: Этот тройственный мир"
                    ]
                  },
                  {
                    id: "got-a3-side",
                    title: "3. Дополнительные задания",
                    items: [
                      "По мерке хана", "Выбор отца", "Скрытое в снегах", "Цена страха", "Трижды проклятый"
                    ]
                  },
                  {
                    id: "got-a3-mythic",
                    title: "4. Легендарная история и награды",
                    items: [
                      "Неугасимое пламя",
                      "Награда: Техника «Путь огня»",
                      "Награда: Маска «Чистота войны»",
                      "Награда: Краска «Скорбь Идзанами»"
                    ]
                  },
                  {
                    id: "got-a3-springs",
                    title: "5. Горячие источники (3/3)",
                    items: [
                      "Горячий источник в предгорьях Дзито",
                      "Горячий источник Моримаэ",
                      "Горячий источник Белого тумана"
                    ]
                  },
                  {
                    id: "got-a3-bamboo",
                    title: "5. Бамбуковые стойки (3/3)",
                    items: [
                      "Бамбуковая стойка Бесконечного леса",
                      "Бамбуковая стойка Кин",
                      "Бамбуковая стойка Саго"
                    ]
                  },
                  {
                    id: "got-a3-shrines",
                    title: "5. Синтоистские святилища (3/3)",
                    items: [
                      "Святилище Журавлиного пика",
                      "Святилище Морозного утёса",
                      "Святилище Снежной вершины"
                    ]
                  },
                  {
                    id: "got-a3-fox",
                    title: "5. Лисьи норы (10/10)",
                    items: numbered("Лисья нора", 10)
                  },
                  {
                    id: "got-a3-haiku",
                    title: "5. Хокку (3 + 1 сюжетное)",
                    items: [
                      "Хокку Дзёгаку", "Хокку Кин", "Хокку Саго",
                      "Сюжетное: Хокку в задании «История господина Симуры»"
                    ]
                  },
                  {
                    id: "got-a3-artifacts",
                    title: "5. Монгольские артефакты (16/16)",
                    items: [
                      "Керамическая посуда", "Огненное копьё", "Порох", "Шкура зверя", "Хвачха",
                      "Маска Махакалы", "Молочный кувшин", "Монгольский шлем", "Монгольское копьё",
                      "Монгольские монеты", "Онгон", "Овоо", "Клетка для пленника", "Кубчур",
                      "Осадные орудия", "Солдатские припасы"
                    ]
                  },
                  {
                    id: "got-a3-records",
                    title: "5. Записи (8/8)",
                    items: [
                      "Разговоры с ханом №9", "Разговоры с ханом №10", "Разговоры с ханом №11",
                      "Крик о помощи", "Прощание", "Госпожа Хана", "Лавка красильщика", "Приглядывай за ней"
                    ]
                  },
                  {
                    id: "got-a3-crickets",
                    title: "5. Поющие сверчки (3/3)",
                    items: numbered("Сверчок", 3)
                  },
                  {
                    id: "got-a3-banners",
                    title: "5. Знамёна сасимоно (18/18)",
                    items: numbered("Знамя", 18)
                  },
                  {
                    id: "got-a3-pillars",
                    title: "5. Столпы чести (7/7)",
                    items: [
                      "Столп чести — набор меча «Лазурный дракон»",
                      "Столп чести — набор меча «Тайный лес»",
                      "Столп чести — набор меча «Страж острова»",
                      "Столп чести — набор меча «Полуночные огни»",
                      "Столп чести — набор меча «Гнев сёгуна»",
                      "Столп чести — набор меча «Хитрость тануки»",
                      "Столп чести — набор меча «Хвост тануки»"
                    ]
                  },
                  {
                    id: "got-a3-lighthouses",
                    title: "5. Маяки (3/3)",
                    items: ["Маяк Дзёгаку", "Маяк Кин", "Маяк Саго"]
                  },
                  {
                    id: "got-a3-vanity",
                    title: "5. Предметы внешнего вида (6/6)",
                    items: [
                      "Повязка изогнутого серпа", "Костяная маска скорби", "Синяя повязка из Саго",
                      "Взор Сэйрю", "Месть скелета", "Тэнгай"
                    ]
                  },
                  {
                    id: "got-a3-territories",
                    title: "6. Монгольские территории и места (16 + 6)",
                    items: [
                      "Форпост: Лагерь генерала Барта", "Форпост: Лагерь генерала Догшина",
                      "Лагерь: Гарнизон Горьких холмов", "Лагерь: Заброшенная шахта",
                      "Лагерь: Перекрёсток Замёрзшего леса", "Лагерь: Замёрзшая смотровая площадка",
                      "Лагерь: Пост охраны Высокой точки", "Лагерь: Перекрёсток Ледяного леса",
                      "Лагерь: Горный перевал", "Лагерь: Шёлковая ферма",
                      "Лагерь: Смотровая площадка «Край сумерек»", "Лагерь: Деревня Белого водопада",
                      "Ферма: Китобойная деревня Кавачи", "Ферма: Пивоварня Моримаэ",
                      "Территория: Застава в горах", "Территория: Рыбацкая деревня Идзуми",
                      "Место: Храм Кедра", "Место: Храм Дзёгаку", "Место: Деревня Идзуми",
                      "Место: Святилище Кин", "Место: Мельница Саго", "Место: Переправа Кубара"
                    ]
                  },
                  {
                    id: "got-a3-final",
                    title: "7–8. Трофеи 3-го акта и проверка завершения",
                    items: [
                      "Союз изгнанников — воссоединиться с союзниками на севере",
                      "Конец правителя — встретиться с ханом",
                      "Моно-но аварэ — завершить историю Дзина",
                      "Массовое выселение — освободить 7 территорий Камиагаты",
                      "Новое безопасное убежище — освободить все территории Камиагаты",
                      "Великий освободитель — освободить весь остров Цусима",
                      "Проверка: все сюжетные, побочные, персонажные и легендарные задания завершены",
                      "Проверка: все коллекционные предметы и активности Камиагаты собраны"
                    ]
                  }
                ]
              }
            ]
          },
          {
            id: "got-trophies",
            title: "Трофеи и Платина",
            acts: [
              {
                id: "got-tr-act",
                title: "Платина и Сюжет (1 + 13 трофеев)",
                groups: [
                  {
                    id: "got-tr-plat",
                    title: "Платина",
                    items: ["Живая легенда — получить все остальные трофеи игры"]
                  },
                  {
                    id: "got-tr-s1",
                    title: "Сюжет — Акт 1 (5)",
                    items: [
                      "1. Лидер клана", "2. Призрак", "3. Удар молнии", "4. Кровь и сталь", "5. Путь воина"
                    ]
                  },
                  {
                    id: "got-tr-s2",
                    title: "Сюжет — Акт 2 (5)",
                    items: [
                      "6. Освободитель Ярикавы", "7. Тени прошлого", "8. Цена чести", "9. На распутье", "10. Буря над островом"
                    ]
                  },
                  {
                    id: "got-tr-s3",
                    title: "Сюжет — Акт 3 (3)",
                    items: [
                      "11. Союз изгнанников", "12. Конец правителя", "13. Моно-но аварэ"
                    ]
                  }
                ]
              },
              {
                id: "got-tr-other",
                title: "Боевые (9), Зачистка (11), Истории (6), Освобождение (7) и Секреты (8)",
                groups: [
                  {
                    id: "got-tr-combat",
                    title: "Боевые (9)",
                    items: [
                      "1. Мастер всех стоек", "2. Призрачный клинок", "3. Смерть из тени",
                      "4. Противостояние", "5. Искусство парирования", "6. Неудержимый клинок",
                      "7. Дуэлянт", "8. Стрелок", "9. Хозяин стихий"
                    ]
                  },
                  {
                    id: "got-tr-cleanup",
                    title: "Зачистка карты (11)",
                    items: [
                      "1. Скромный поклон", "2. По стопам предков", "3. Согревающий пар",
                      "4. Быстрее ветра", "5. Друг лис", "6. Поэт Цусимы",
                      "7. Легенды Цусимы", "8. Хранитель воспоминаний", "9. Трофеи войны",
                      "10. Мастер клинка", "11. Полный арсенал"
                    ]
                  },
                  {
                    id: "got-tr-tales",
                    title: "Истории и побочные задания (6)",
                    items: [
                      "1. Союзники Цусимы", "2. Помощник народа", "3. Верный ученик",
                      "4. Справедливость госпожи Масако", "5. Путь монаха", "6. Узы семьи"
                    ]
                  },
                  {
                    id: "got-tr-lib",
                    title: "Освобождение территорий (7)",
                    items: [
                      "1. Освобождение Идзухары", "2. Освобождение Тоётамы", "3. Массовое выселение",
                      "4. Новое безопасное убежище", "5. Зачистка тылов", "6. Падение форпостов",
                      "7. Великий освободитель"
                    ]
                  },
                  {
                    id: "got-tr-sec",
                    title: "Секреты и режимы (8)",
                    items: [
                      "1. Высшая точка", "2. Сыграй мне песню", "3. Почтение павшим",
                      "4. Неожиданная встреча", "5. Прыжок веры", "6. По следам легенд",
                      "7. Мастер маскировки", "8. Истинный дух острова"
                    ]
                  }
                ]
              }
            ]
          }
        ]
      };

      // Чек-лист Grand Theft Auto III (GTA 3)
      const GTA_III = {
        id: "gta-iii",
        title: "Grand Theft Auto III (GTA 3)",
        subtitle: "Портленд, Стаунтон-Айленд, Шорсайд-Вейл, 100% зачистка и трофеи",
        badge: "100% + Трофеи",
        category: "Open World / Action",
        tabs: [
          {
            id: "gta3-portland",
            title: "1. Портленд",
            acts: [
              {
                id: "gta3-p-story",
                title: "Сюжетные задания — Портленд",
                groups: [
                  {
                    id: "gta3-p-intro-luigi",
                    title: "Вступление и Луиджи Готерелли",
                    items: [
                      "Поездка (Give Me Liberty)",
                      "Луиджины девчонки (Luigi's Girls)",
                      "Не бросай Мисти (Don't Spank Ma Bitch Up)",
                      "Наезд на мафиози (Drive Misty For Me)",
                      "Помповый экшн (Pump Action Pimp)",
                      "Громила (The Fuzz Ball)"
                    ]
                  },
                  {
                    id: "gta3-p-toni",
                    title: "Тони Сиприани",
                    items: [
                      "Убрать соседа (Taking Out the Laundry)",
                      "Взрыв на парковке (The Pick-Up)",
                      "Сальваторе заказывает (Salvatore's Called a Meeting)",
                      "Триады и разборки (Triads and Tribulations)",
                      "Резня в прачечной (Blow Fish)"
                    ]
                  },
                  {
                    id: "gta3-p-joey",
                    title: "Джои Леоне",
                    items: [
                      "Мобила Майка (Mike Lips Last Lunch)",
                      "Прощай, Горбун (Farewell 'Chunky' Lee Chong)",
                      "Исчезновение (Van Heist)",
                      "Укрощение строптивого (Cipriani's Chauffeur)",
                      "Смертельный груз (Dead Skunk in the Trunk)",
                      "Ограбление банка (The Getaway)"
                    ]
                  },
                  {
                    id: "gta3-p-salvatore",
                    title: "Сальваторе Леоне",
                    items: [
                      "Опасный груз (Chaperone)",
                      "Удар в спину (Cutting the Grass)",
                      "Бомба на пристани (Bomb Da Base: Act I)",
                      "Бомба на пристани: Акт II (Bomb Da Base: Act II)",
                      "Последняя просьба (Last Requests)"
                    ]
                  }
                ]
              },
              {
                id: "gta3-p-extra",
                title: "Активности и коллекционки — Портленд",
                groups: [
                  {
                    id: "gta3-p-phones",
                    title: "Таксофоны (Марти Чонкс и Эль Бурро)",
                    items: [
                      "Марти: Кража (The Crook)",
                      "Марти: Воры (The Thieves)",
                      "Марти: Жена (Her Lover)",
                      "Марти: Ужин с боссом (His Wife)",
                      "Эль Бурро: Вояж по Портленду (Turismo)"
                    ]
                  },
                  {
                    id: "gta3-p-jobs",
                    title: "Службы, авто и RC",
                    items: [
                      "Парамедик (35 пассажиров)",
                      "Полицейский беспредел (10–20 целей)",
                      "Пожарный (20 пожаров в районе)",
                      "Таксист (100 клиентов всего)",
                      "Кран импорта/экспорта в доках Портленда",
                      "Радиоуправляемые машинки (RC Toyz — Портленд)"
                    ]
                  },
                  {
                    id: "gta3-p-collect",
                    title: "Скрытые пакеты (33), рампэджи (6) и прыжки",
                    items: [
                      "Собрать все 33 скрытых пакета в Портленде",
                      "Рампэдж №1 (Портленд)", "Рампэдж №2 (Портленд)", "Рампэдж №3 (Портленд)",
                      "Рампэдж №4 (Портленд)", "Рампэдж №5 (Портленд)", "Рампэдж №6 (Портленд)",
                      "Выполнить уникальные прыжки в Портленде"
                    ]
                  }
                ]
              }
            ]
          },
          {
            id: "gta3-staunton",
            title: "2. Стаунтон-Айленд",
            acts: [
              {
                id: "gta3-s-story",
                title: "Сюжетные задания — Стаунтон-Айленд",
                groups: [
                  {
                    id: "gta3-s-asuka",
                    title: "Асука Касэн",
                    items: [
                      "Сайонара, Сальваторе (Sayonara Salvatore)",
                      "Под прикрытием (Under Surveillance)",
                      "Папаша (Paparazzi Purge)",
                      "Удар по «Якудза» (Payday For Ray)",
                      "Два лица (Two-Faced Tanner)"
                    ]
                  },
                  {
                    id: "gta3-s-kenji",
                    title: "Кенджи Касэн",
                    items: [
                      "Кандидат (Kanbu Bust-Out)",
                      "Блокировка (Grand Theft Auto)",
                      "Сделка (Deal Steal)",
                      "Дёргая за ниточки (Shima)"
                    ]
                  },
                  {
                    id: "gta3-s-ray",
                    title: "Рэй Мачовски",
                    items: [
                      "Тишина (Silence the Sneak)",
                      "Оружие для бегства (Arms Shortage)",
                      "Доказательства (Evidence Dash)",
                      "Потерянный в сети (Gone Fishing)",
                      "В пламени (Plaster Blaster)"
                    ]
                  },
                  {
                    id: "gta3-s-love",
                    title: "Дональд Лав (часть 1)",
                    items: [
                      "Освободитель (Liberator)",
                      "Вакханалия (Waka-Gashira Wipeout!)",
                      "Кенджи должен умереть (A Drop in the Ocean)"
                    ]
                  }
                ]
              },
              {
                id: "gta3-s-extra",
                title: "Активности и коллекционки — Стаунтон-Айленд",
                groups: [
                  {
                    id: "gta3-s-phones",
                    title: "Таксофон (Кинг Куртни) и RC",
                    items: [
                      "Кинг Куртни: Курьер (Bling-Bling Scramble)",
                      "Кинг Куртни: Смерть с небес (Uzi Rider)",
                      "Кинг Куртни: Перестрелка (Gangcar Round-up)",
                      "Кинг Куртни: Кровавый счёт (Kingdom Come)",
                      "Радиоуправляемые машинки (RC Toyz — Стаунтон)"
                    ]
                  },
                  {
                    id: "gta3-s-collect",
                    title: "Скрытые пакеты (36), рампэджи (7) и прыжки",
                    items: [
                      "Собрать все 36 скрытых пакетов на Стаунтон-Айленде",
                      "Рампэджи на Стаунтон-Айленде (7 шт.)",
                      "Выполнить уникальные прыжки на Стаунтон-Айленде"
                    ]
                  }
                ]
              }
            ]
          },
          {
            id: "gta3-shoreside",
            title: "3. Шорсайд-Вейл",
            acts: [
              {
                id: "gta3-sv-story",
                title: "Сюжетные задания — Шорсайд-Вейл",
                groups: [
                  {
                    id: "gta3-sv-love-ray",
                    title: "Дональд Лав (часть 2) и Рэй",
                    items: [
                      "Большой куш (Grand Theft Aero)",
                      "Сопровождение (Escort Service)",
                      "Саботаж (Decoy)",
                      "Любовь и смерть (Love 'Em and Leave 'Em)",
                      "Сделка с картелем (Marked Man)"
                    ]
                  },
                  {
                    id: "gta3-sv-asuka-final",
                    title: "Асука и финал",
                    items: [
                      "Каталина наносит ответный удар (Espresso-2-Go!)",
                      "Охота на предателя (S.A.M.)",
                      "Обмен (The Exchange)"
                    ]
                  }
                ]
              },
              {
                id: "gta3-sv-extra",
                title: "Активности и коллекционки — Шорсайд-Вейл",
                groups: [
                  {
                    id: "gta3-sv-phones-cars",
                    title: "Ди-Айс, автосалон и RC",
                    items: [
                      "Ди-Айс: Катафалк (Rumble)",
                      "Список машин в автосалоне Шорсайд-Вейла",
                      "Радиоуправляемые машинки (RC Toyz — Шорсайд-Вейл)"
                    ]
                  },
                  {
                    id: "gta3-sv-collect",
                    title: "Скрытые пакеты (31), рампэджи (7) и прыжки",
                    items: [
                      "Собрать все 31 скрытый пакет в Шорсайд-Вейле",
                      "Рампэджи в Шорсайд-Вейле (7 шт.)",
                      "Выполнить уникальные прыжки в Шорсайд-Вейле"
                    ]
                  }
                ]
              }
            ]
          },
          {
            id: "gta3-100-trophies",
            title: "4. 100% и трофеи",
            acts: [
              {
                id: "gta3-100",
                title: "100% прохождение и трофеи GTA III",
                groups: [
                  {
                    id: "gta3-100-req",
                    title: "Условия 100% зачистки",
                    items: [
                      "Пройти все основные сюжетные задания",
                      "Пройти все задания на таксофонах",
                      "Собрать все 100 скрытых пакетов",
                      "Пройти все 20 рампэджей",
                      "Выполнить все 20 уникальных прыжков",
                      "Пройти все 4 миссии на RC-машинках",
                      "Пройти все 4 внедорожные гонки",
                      "Завершить миссии парамедика, пожарного и полицейского",
                      "Перевезти 100 пассажиров на такси",
                      "Сдать машины на кран в Портленде и в автосалон в Шорсайд-Вейле"
                    ]
                  },
                  {
                    id: "gta3-tr-list",
                    title: "Ключевые трофеи и достижения",
                    items: [
                      "Полное доминирование (100% прохождения)",
                      "Король Либерти-Сити (завершить сюжет)",
                      "Скрытный охотник (собрать все 100 скрытых пакетов)",
                      "Ярость на улицах (пройти все 20 рампэджей)",
                      "Полёт над городом (выполнить все 20 уникальных прыжков)",
                      "На страже порядка / Скорая помощь / Пожарный надзор",
                      "Уличный гонщик / Импорт-экспорт",
                      "Мастер хедшотов / Взрывная волна"
                    ]
                  }
                ]
              }
            ]
          }
        ]
      };

      const UPCOMING_CARDS = [
        {
          title: "Новые игры в каталог",
          tag: "Скоро",
          desc: "Сюда будем добавлять следующие полные чек-листы по играм."
        },
        {
          title: "Облачная синхронизация",
          tag: "В планах",
          desc: "Позже можно подключить серверную базу, чтобы входить в свой аккаунт с любого устройства."
        }
      ];

      const FORUM_CATEGORIES = [
        "Общее",
        "Ghost of Tsushima",
        "GTA 3",
        "Помощь и тактики",
        "Предложения"
      ];

      function seedDefaultForumThreads() {
        return [
          {
            id: "thread-got-1",
            title: "Как быстрее закрыть все знамёна сасимоно и лисьи норы в Ghost of Tsushima?",
            category: "Ghost of Tsushima",
            authorId: "demo-jin",
            authorName: "Дзин Сакай",
            createdAt: "2026-11-16T14:20:00.000Z",
            body: "Поделитесь удобным маршрутом: стоит ли добивать коллекционки по актам сразу или оставить часть до открытия полного снаряжения и направляющего ветра? В Акре 1 уже почти всё закрыл.",
            replies: [
              {
                id: "rep-101",
                authorId: "demo-seeker",
                authorName: "Искатель 100%",
                createdAt: "2026-11-16T15:05:00.000Z",
                text: "Я закрываю максимум по актам, пока нахожусь в регионе, а точечные знамёна и лисьи норы удобно добивать через направляющий ветер из карты. С чек-листом тут реально проще не сбиться со счёта."
              }
            ]
          },
          {
            id: "thread-gta3-1",
            title: "Советы по миссии парамедика и картелям в GTA 3 на 100%",
            category: "GTA 3",
            authorId: "demo-claude",
            authorName: "Клод из Либерти",
            createdAt: "2026-11-17T18:40:00.000Z",
            body: "В Портленде лучше сделать парамедика в самом начале, пока банды мафии и триад не стали агрессивными после сюжетных поворотов. Кто как проходил рампэджи на Стаунтоне?",
            replies: [
              {
                id: "rep-102",
                authorId: "demo-jin",
                authorName: "Дзин Сакай",
                createdAt: "2026-11-17T19:12:00.000Z",
                text: "Поддерживаю: парамедик в Портленде до обострения отношений с мафией экономит кучу нервов. На Стаунтоне рампэджи хорошо идут с огнемётом и гранатами по скоплениям банд."
              }
            ]
          },
          {
            id: "thread-help-1",
            title: "Какие чек-листы по играм добавить следующими в каталог?",
            category: "Предложения",
            authorId: "demo-seeker",
            authorName: "Искатель 100%",
            createdAt: "2026-11-18T11:15:00.000Z",
            body: "У нас уже есть Ghost of Tsushima и GTA III. Напишите в ответах, какие игры с большими списками заданий, коллекционок или платиной стоит собрать дальше.",
            replies: []
          }
        ];
      }

      function defaultState() {
        return {
          route: { view: "catalog", checklistId: null, tabId: null, threadId: null },
          checked: {},
          collapsed: {},
          customChecklists: [],
          users: [],
          currentUserId: null,
          forumThreads: seedDefaultForumThreads()
        };
      }

      function loadState() {
        const base = defaultState();
        const raw = readStorage();
        if (!raw) return base;
        try {
          const parsed = JSON.parse(raw);
          const viewAllowed = ["catalog", "checklist", "forum", "thread", "profile"];
          return {
            route: parsed.route && typeof parsed.route === "object"
              ? {
                  view: viewAllowed.includes(parsed.route.view) ? parsed.route.view : "catalog",
                  checklistId: parsed.route.checklistId || null,
                  tabId: parsed.route.tabId || null,
                  threadId: parsed.route.threadId || null
                }
              : base.route,
            checked: parsed.checked && typeof parsed.checked === "object" ? parsed.checked : {},
            collapsed: parsed.collapsed && typeof parsed.collapsed === "object" ? parsed.collapsed : {},
            customChecklists: Array.isArray(parsed.customChecklists) ? parsed.customChecklists : [],
            users: Array.isArray(parsed.users) ? parsed.users : [],
            currentUserId: typeof parsed.currentUserId === "string" ? parsed.currentUserId : null,
            forumThreads: Array.isArray(parsed.forumThreads) && parsed.forumThreads.length > 0
              ? parsed.forumThreads
              : seedDefaultForumThreads()
          };
        } catch (err) {
          return base;
        }
      }

      let state = loadState();

      function saveState() {
        writeStorage(JSON.stringify(state));
        syncStorageIndicator();
        syncAuthHeader();
      }

      function getCurrentUser() {
        if (!state.currentUserId) return null;
        return state.users.find((u) => u.id === state.currentUserId) || null;
      }

      function syncAuthHeader() {
        const dot = document.getElementById("authStatusDot");
        const label = document.getElementById("authStatusLabel");
        const user = getCurrentUser();
        if (!dot || !label) return;
        if (user) {
          dot.className = "h-2 w-2 rounded-full bg-[#10b981]";
          label.textContent = user.username;
        } else {
          dot.className = "h-2 w-2 rounded-full bg-[#f59e0b]";
          label.textContent = "Войти / Профиль";
        }

        const catBtn = document.getElementById("navCatalogBtn");
        const forumBtn = document.getElementById("navForumBtn");
        const isForumActive = state.route.view === "forum" || state.route.view === "thread";
        const isCatalogActive = state.route.view === "catalog" || state.route.view === "checklist";

        if (catBtn) {
          catBtn.className = isCatalogActive
            ? "rounded-lg bg-[#e11d48] px-3 py-1.5 text-xs font-semibold text-white transition"
            : "rounded-lg px-3 py-1.5 text-xs font-semibold text-gray-300 transition hover:bg-white/10 hover:text-white";
        }
        if (forumBtn) {
          forumBtn.className = isForumActive
            ? "rounded-lg bg-[#e11d48] px-3 py-1.5 text-xs font-semibold text-white transition"
            : "rounded-lg px-3 py-1.5 text-xs font-semibold text-gray-300 transition hover:bg-white/10 hover:text-white";
        }
      }

      // Модалка авторизации / регистрации
      const authModal = document.getElementById("authModal");
      const authErrorBox = document.getElementById("authErrorBox");
      const loginForm = document.getElementById("loginForm");
      const registerForm = document.getElementById("registerForm");

      function setAuthError(msg) {
        if (!authErrorBox) return;
        if (!msg) {
          authErrorBox.textContent = "";
          authErrorBox.classList.add("hidden");
        } else {
          authErrorBox.textContent = msg;
          authErrorBox.classList.remove("hidden");
        }
      }

      function switchAuthTab(mode) {
        authModalMode = mode;
        setAuthError("");
        const loginTab = document.getElementById("authTabLoginBtn");
        const regTab = document.getElementById("authTabRegisterBtn");

        if (mode === "login") {
          loginForm.classList.remove("hidden");
          registerForm.classList.add("hidden");
          loginTab.className = "rounded-lg bg-[#e11d48] py-2 text-xs font-semibold text-white transition";
          regTab.className = "rounded-lg py-2 text-xs font-semibold text-gray-400 transition hover:text-white";
        } else {
          loginForm.classList.add("hidden");
          registerForm.classList.remove("hidden");
          regTab.className = "rounded-lg bg-[#e11d48] py-2 text-xs font-semibold text-white transition";
          loginTab.className = "rounded-lg py-2 text-xs font-semibold text-gray-400 transition hover:text-white";
        }
      }

      function openAuthModal(mode = "login") {
        switchAuthTab(mode);
        authModal.classList.remove("hidden");
        authModal.classList.add("flex");
        const focusEl = mode === "login"
          ? document.getElementById("loginIdentifierInput")
          : document.getElementById("regUsernameInput");
        if (focusEl) focusEl.focus();
      }

      function closeAuthModal() {
        authModal.classList.add("hidden");
        authModal.classList.remove("flex");
        setAuthError("");
      }

      document.getElementById("closeAuthModalBtn").addEventListener("click", closeAuthModal);
      document.getElementById("authTabLoginBtn").addEventListener("click", () => switchAuthTab("login"));
      document.getElementById("authTabRegisterBtn").addEventListener("click", () => switchAuthTab("register"));
      authModal.addEventListener("click", (e) => {
        if (e.target === authModal) closeAuthModal();
      });

      loginForm.addEventListener("submit", (e) => {
        e.preventDefault();
        setAuthError("");
        const ident = document.getElementById("loginIdentifierInput").value.trim().toLowerCase();
        const pass = document.getElementById("loginPasswordInput").value;

        if (!ident || !pass) {
          setAuthError("Заполните оба поля для входа.");
          return;
        }

        const matched = state.users.find(
          (u) =>
            u.username.toLowerCase() === ident ||
            u.handle.toLowerCase() === ident
        );

        if (!matched) {
          setAuthError("Аккаунт с таким никнеймом или handle/email не найден. Вы можете зарегистрироваться или войти в демо-профиль.");
          return;
        }

        if (matched.password !== pass) {
          setAuthError("Неверный пароль.");
          return;
        }

        state.currentUserId = matched.id;
        saveState();
        closeAuthModal();
        loginForm.reset();
        showToast(`С возвращением, ${matched.username}!`);
        render();
      });

      registerForm.addEventListener("submit", (e) => {
        e.preventDefault();
        setAuthError("");
        const username = document.getElementById("regUsernameInput").value.trim();
        const handle = document.getElementById("regHandleInput").value.trim();
        const password = document.getElementById("regPasswordInput").value;
        const bio = document.getElementById("regBioInput").value.trim();

        if (username.length < 2 || username.length > 24) {
          setAuthError("Никнейм должен содержать от 2 до 24 символов.");
          return;
        }
        if (handle.length < 3) {
          setAuthError("Укажите корректный email или @handle.");
          return;
        }
        if (password.length < 4) {
          setAuthError("Пароль должен быть не короче 4 символов.");
          return;
        }

        const exists = state.users.some(
          (u) =>
            u.username.toLowerCase() === username.toLowerCase() ||
            u.handle.toLowerCase() === handle.toLowerCase()
        );
        if (exists) {
          setAuthError("Пользователь с таким никнеймом или handle/email уже существует.");
          return;
        }

        const newUser = {
          id: `user-${Date.now().toString(36)}`,
          username,
          handle,
          password,
          provider: "local",
          bio: bio || "Собираю 100% прохождение и общаюсь на форуме Чек-лист Хаба.",
          joinedAt: new Date().toISOString()
        };

        state.users.push(newUser);
        state.currentUserId = newUser.id;
        saveState();
        closeAuthModal();
        registerForm.reset();
        showToast(`Профиль «${newUser.username}» создан!`);
        state.route = { view: "profile", checklistId: null, tabId: null, threadId: null };
        render();
      });

      // Hook для подключения реального OAuth (Supabase / Firebase) при переходе на облачный бэкенд
      const CLOUD_GOOGLE_AUTH_HOOK = null;

      async function handleGoogleQuickSignIn() {
        setAuthError("");
        try {
          if (typeof CLOUD_GOOGLE_AUTH_HOOK === "function") {
            const cloudProfile = await CLOUD_GOOGLE_AUTH_HOOK();
            if (!cloudProfile || !cloudProfile.email) {
              setAuthError("Не удалось получить профиль из облачной авторизации Google.");
              return;
            }
            let cloudUser = state.users.find(
              (u) => u.handle.toLowerCase() === String(cloudProfile.email).toLowerCase()
            );
            if (!cloudUser) {
              cloudUser = {
                id: `google-${Date.now().toString(36)}`,
                username: String(cloudProfile.name || "Игрок Google").slice(0, 24),
                handle: String(cloudProfile.email),
                password: "",
                provider: "google",
                bio: "Вход выполнен через Google-аккаунт.",
                joinedAt: new Date().toISOString()
              };
              state.users.push(cloudUser);
            }
            state.currentUserId = cloudUser.id;
            saveState();
            closeAuthModal();
            showToast(`Вход через Google выполнен: ${cloudUser.username}`);
            render();
            return;
          }

          // Локальный / демо-режим быстрой регистрации и входа через Google
          const googleHandle = "player.google@gmail.com";
          let googleUser = state.users.find(
            (u) => u.provider === "google" || u.handle.toLowerCase() === googleHandle
          );
          if (!googleUser) {
            googleUser = {
              id: "google-demo-player",
              username: "Игрок Google",
              handle: googleHandle,
              password: "",
              provider: "google",
              bio: "Быстрый профиль через Google — прохожу игры на 100% и общаюсь на форуме.",
              joinedAt: new Date().toISOString()
            };
            state.users.push(googleUser);
          }
          state.currentUserId = googleUser.id;
          saveState();
          closeAuthModal();
          showToast(`Быстрый вход через Google: ${googleUser.username}`);
          render();
        } catch (err) {
          setAuthError("Ошибка при быстром входе через Google. Попробуйте ещё раз.");
        }
      }

      document.getElementById("googleQuickSignInBtn").addEventListener("click", handleGoogleQuickSignIn);

      document.getElementById("quickDemoLoginBtn").addEventListener("click", () => {
        let demo = state.users.find((u) => u.id === "demo-seeker");
        if (!demo) {
          demo = {
            id: "demo-seeker",
            username: "Искатель 100%",
            handle: "@seeker_100",
            password: "demo",
            provider: "demo",
            bio: "Быстрый демо-профиль для тестов чек-листов, форума и профиля.",
            joinedAt: new Date().toISOString()
          };
          state.users.push(demo);
        }
        state.currentUserId = demo.id;
        saveState();
        closeAuthModal();
        showToast("Вход в демо-профиль «Искатель 100%» выполнен");
        render();
      });

      // Работа с чек-листами и прогрессом
      function allChecklists() {
        return [GHOST_OF_TSUSHIMA, GTA_III, ...state.customChecklists];
      }

      function findChecklist(id) {
        return allChecklists().find((c) => c.id === id) || null;
      }

      function makeKey(checklistId, groupId, idx) {
        return `${checklistId}::${groupId}::${idx}`;
      }

      function isItemChecked(checklistId, groupId, idx) {
        return Boolean(state.checked[makeKey(checklistId, groupId, idx)]);
      }

      function setItemChecked(checklistId, groupId, idx, val) {
        const key = makeKey(checklistId, groupId, idx);
        if (val) state.checked[key] = true;
        else delete state.checked[key];
        saveState();
      }

      function getChecklistProgress(cl) {
        let total = 0;
        let done = 0;
        for (const tab of cl.tabs || []) {
          for (const act of tab.acts || []) {
            for (const g of act.groups || []) {
              const n = (g.items || []).length;
              total += n;
              for (let i = 0; i < n; i++) {
                if (isItemChecked(cl.id, g.id, i)) done++;
              }
            }
          }
        }
        return { total, done, pct: total ? Math.round((done / total) * 100) : 0 };
      }

      function getTabProgress(cl, tab) {
        let total = 0;
        let done = 0;
        for (const act of tab.acts || []) {
          for (const g of act.groups || []) {
            const n = (g.items || []).length;
            total += n;
            for (let i = 0; i < n; i++) {
              if (isItemChecked(cl.id, g.id, i)) done++;
            }
          }
        }
        return { total, done, pct: total ? Math.round((done / total) * 100) : 0 };
      }

      function getGroupProgress(cl, g) {
        const total = (g.items || []).length;
        let done = 0;
        for (let i = 0; i < total; i++) {
          if (isItemChecked(cl.id, g.id, i)) done++;
        }
        return { total, done, pct: total ? Math.round((done / total) * 100) : 0 };
      }

      function getUserForumStats(user) {
        if (!user) return { threadsCount: 0, repliesCount: 0 };
        let threadsCount = 0;
        let repliesCount = 0;
        for (const t of state.forumThreads || []) {
          if (t.authorId === user.id || t.authorName === user.username) {
            threadsCount++;
          }
          for (const r of t.replies || []) {
            if (r.authorId === user.id || r.authorName === user.username) {
              repliesCount++;
            }
          }
        }
        return { threadsCount, repliesCount };
      }

      // Экран каталога
      function renderCatalog() {
        const root = document.getElementById("appRoot");
        const lists = allChecklists();

        let totalAll = 0;
        let doneAll = 0;
        for (const cl of lists) {
          const p = getChecklistProgress(cl);
          totalAll += p.total;
          doneAll += p.done;
        }
        const pctAll = totalAll ? Math.round((doneAll / totalAll) * 100) : 0;

        const cards = lists
          .map((cl) => {
            const p = getChecklistProgress(cl);
            const isCustom = cl.id !== "ghost-of-tsushima" && cl.id !== "gta-iii";
            return `
              <article
                data-open-checklist="${escapeHtml(cl.id)}"
                class="flex cursor-pointer flex-col justify-between gap-4 rounded-2xl border border-white/10 bg-[#14161c] p-5 transition hover:-translate-y-0.5 hover:border-white/25 hover:bg-[#191c24]"
              >
                <div>
                  <div class="mb-2 flex flex-wrap gap-1.5">
                    <span class="rounded-full bg-[#e11d48]/15 px-2.5 py-0.5 text-[11px] font-semibold text-rose-300">
                      ${escapeHtml(cl.category || "Чек-лист")}
                    </span>
                    ${cl.badge ? `<span class="rounded-full bg-[#f59e0b]/15 px-2.5 py-0.5 text-[11px] font-semibold text-amber-300">${escapeHtml(cl.badge)}</span>` : ""}
                  </div>
                  <h3 class="text-lg font-bold text-white">${escapeHtml(cl.title)}</h3>
                  <p class="mt-1 text-xs leading-relaxed text-gray-400">${escapeHtml(cl.subtitle || "")}</p>
                </div>

                <div>
                  <div class="mb-1.5 flex items-center justify-between text-xs text-gray-400">
                    <span>Выполнено: <strong class="text-white">${p.done}</strong> / ${p.total}</span>
                    <span class="font-semibold text-gray-200">${p.pct}%</span>
                  </div>
                  <div class="h-2 w-full overflow-hidden rounded-full bg-white/10">
                    <div class="h-full rounded-full bg-gradient-to-r from-[#e11d48] via-[#f59e0b] to-[#10b981] transition-all duration-300" style="width:${p.pct}%"></div>
                  </div>
                  <div class="mt-4 flex items-center justify-between gap-2">
                    <button
                      type="button"
                      data-open-btn="${escapeHtml(cl.id)}"
                      class="rounded-xl bg-[#e11d48] px-3.5 py-2 text-xs font-semibold text-white transition hover:bg-rose-500"
                    >
                      Открыть чек-лист
                    </button>
                    ${
                      isCustom
                        ? `<button type="button" data-delete-custom="${escapeHtml(cl.id)}" class="rounded-xl border border-red-500/30 bg-red-500/10 px-3 py-2 text-xs font-medium text-red-300 hover:bg-red-500/20">Удалить</button>`
                        : ""
                    }
                  </div>
                </div>
              </article>
            `;
          })
          .join("");

        const upcoming = UPCOMING_CARDS.map(
          (u) => `
            <article class="rounded-2xl border border-white/10 bg-[#14161c]/70 p-5 opacity-80">
              <span class="inline-block rounded-full bg-[#f59e0b]/15 px-2.5 py-0.5 text-[11px] font-semibold text-amber-300">${escapeHtml(u.tag)}</span>
              <h3 class="mt-2 text-base font-bold text-white">${escapeHtml(u.title)}</h3>
              <p class="mt-1 text-xs text-gray-400">${escapeHtml(u.desc)}</p>
            </article>
          `
        ).join("");

        root.innerHTML = `
          <section class="rounded-2xl border border-white/10 bg-gradient-to-br from-[#e11d48]/20 via-[#14161c] to-[#f59e0b]/10 p-5 shadow-xl sm:p-6">
            <div class="flex flex-wrap items-start justify-between gap-4">
              <div class="max-w-2xl">
                <h1 class="text-2xl font-extrabold tracking-tight text-white sm:text-3xl">Каталог чек-листов</h1>
                <p class="mt-1.5 text-sm text-gray-300">
                  Отмечай прохождение по заданиям, коллекционкам и трофеям, обсуждай тактики на форуме и веди свой профиль игрока.
                </p>
              </div>
              <div class="flex flex-wrap gap-2">
                <button
                  id="openForumShortcutBtn"
                  type="button"
                  class="rounded-xl border border-white/15 bg-[#191c24] px-4 py-2.5 text-xs font-semibold text-white transition hover:bg-[#222733]"
                >
                  Перейти на форум (${state.forumThreads.length})
                </button>
                <button
                  id="openCreateModalBtn"
                  type="button"
                  class="rounded-xl bg-[#e11d48] px-4 py-2.5 text-xs font-semibold text-white shadow-lg shadow-rose-950/50 transition hover:bg-rose-500"
                >
                  + Свой чек-лист
                </button>
              </div>
            </div>

            <div class="mt-5 border-t border-white/10 pt-4">
              <div class="mb-2 flex items-center justify-between text-xs text-gray-300">
                <span>Общий прогресс: <strong class="text-white">${doneAll}</strong> из <strong class="text-white">${totalAll}</strong> пунктов</span>
                <span class="font-bold text-white">${pctAll}%</span>
              </div>
              <div class="h-2.5 w-full overflow-hidden rounded-full bg-white/10">
                <div class="h-full rounded-full bg-gradient-to-r from-[#e11d48] via-[#f59e0b] to-[#10b981] transition-all duration-300" style="width:${pctAll}%"></div>
              </div>
            </div>
          </section>

          <div class="mb-3 mt-7 flex items-center justify-between">
            <h2 class="text-lg font-bold text-white">Доступные списки (${lists.length})</h2>
          </div>
          <div class="grid grid-cols-1 gap-4 md:grid-cols-2">${cards}</div>

          <div class="mb-3 mt-8">
            <h2 class="text-base font-bold text-gray-300">В планах</h2>
          </div>
          <div class="grid grid-cols-1 gap-4 sm:grid-cols-2">${upcoming}</div>
        `;

        root.querySelectorAll("[data-open-checklist]").forEach((card) => {
          card.addEventListener("click", () => openChecklist(card.getAttribute("data-open-checklist")));
        });

        root.querySelectorAll("[data-open-btn]").forEach((btn) => {
          btn.addEventListener("click", (e) => {
            e.stopPropagation();
            openChecklist(btn.getAttribute("data-open-btn"));
          });
        });

        root.querySelectorAll("[data-delete-custom]").forEach((btn) => {
          btn.addEventListener("click", (e) => {
            e.stopPropagation();
            const id = btn.getAttribute("data-delete-custom");
            state.customChecklists = state.customChecklists.filter((c) => c.id !== id);
            saveState();
            render();
            showToast("Список удалён");
          });
        });

        document.getElementById("openCreateModalBtn").addEventListener("click", openCreateModal);
        document.getElementById("openForumShortcutBtn").addEventListener("click", () => {
          state.route = { view: "forum", checklistId: null, tabId: null, threadId: null };
          saveState();
          render();
        });
      }

      function openChecklist(id) {
        const cl = findChecklist(id);
        if (!cl) return;
        const firstTab = cl.tabs && cl.tabs[0] ? cl.tabs[0].id : null;
        const keepTab = cl.tabs.some((t) => t.id === state.route.tabId) ? state.route.tabId : firstTab;
        state.route = { view: "checklist", checklistId: cl.id, tabId: keepTab, threadId: null };
        checklistSearch = "";
        checklistFilter = "all";
        pendingResetConfirm = false;
        saveState();
        render();
        window.scrollTo({ top: 0, behavior: "smooth" });
      }

      // Экран конкретного чек-листа
      function renderChecklist() {
        const root = document.getElementById("appRoot");
        const cl = findChecklist(state.route.checklistId) || GHOST_OF_TSUSHIMA;
        const activeTab = cl.tabs.find((t) => t.id === state.route.tabId) || cl.tabs[0];
        if (activeTab && state.route.tabId !== activeTab.id) {
          state.route.tabId = activeTab.id;
          saveState();
        }

        const clProg = getChecklistProgress(cl);
        const tabProg = getTabProgress(cl, activeTab);
        const q = checklistSearch.trim().toLowerCase();

        const tabButtons = cl.tabs
          .map((t) => {
            const p = getTabProgress(cl, t);
            const active = t.id === activeTab.id;
            return `
              <button
                type="button"
                data-tab-btn="${escapeHtml(t.id)}"
                class="flex items-center gap-2 rounded-xl border px-3.5 py-2 text-xs font-semibold transition ${
                  active
                    ? "border-[#e11d48] bg-[#e11d48] text-white shadow-md shadow-rose-950/50"
                    : "border-white/10 bg-[#14161c] text-gray-300 hover:border-white/25 hover:bg-[#191c24]"
                }"
              >
                <span>${escapeHtml(t.title)}</span>
                <span class="rounded-full bg-black/30 px-2 py-0.5 text-[11px]">${p.done}/${p.total}</span>
              </button>
            `;
          })
          .join("");

        const actsMarkup = (activeTab.acts || [])
          .map((act) => {
            const groupsMarkup = (act.groups || [])
              .map((g) => {
                const gp = getGroupProgress(cl, g);
                const collapsed = Boolean(state.collapsed[g.id]);
                const indices = [];

                (g.items || []).forEach((label, idx) => {
                  const done = isItemChecked(cl.id, g.id, idx);
                  const okFilter =
                    checklistFilter === "all" ||
                    (checklistFilter === "todo" && !done) ||
                    (checklistFilter === "done" && done);
                  const okSearch =
                    !q ||
                    String(label).toLowerCase().includes(q) ||
                    String(g.title).toLowerCase().includes(q);
                  if (okFilter && okSearch) indices.push(idx);
                });

                if ((q || checklistFilter !== "all") && indices.length === 0) return "";

                const rows = indices
                  .map((idx) => {
                    const label = g.items[idx];
                    const done = isItemChecked(cl.id, g.id, idx);
                    return `
                      <label class="check-row ${done ? "is-done" : ""} flex cursor-pointer items-start gap-3 rounded-xl px-2.5 py-2 transition hover:bg-white/[0.04]">
                        <input
                          type="checkbox"
                          ${done ? "checked" : ""}
                          data-check-group="${escapeHtml(g.id)}"
                          data-check-idx="${idx}"
                          class="mt-0.5 h-4 w-4 shrink-0 cursor-pointer accent-[#10b981]"
                        />
                        <span class="check-text text-sm leading-snug text-gray-100">${escapeHtml(label)}</span>
                      </label>
                    `;
                  })
                  .join("");

                const allDone = gp.total > 0 && gp.done === gp.total;

                return `
                  <div class="overflow-hidden rounded-2xl border border-white/10 bg-[#14161c]">
                    <div
                      data-toggle-group="${escapeHtml(g.id)}"
                      class="flex cursor-pointer items-center justify-between gap-2 border-b border-white/10 bg-[#191c24]/60 px-4 py-3 select-none hover:bg-[#191c24]"
                    >
                      <div class="flex min-w-0 items-center gap-2">
                        <span class="chev ${collapsed ? "is-collapsed" : ""} text-[11px] text-gray-400 transition-transform">▼</span>
                        <span class="truncate text-sm font-semibold text-white">${escapeHtml(g.title)}</span>
                      </div>
                      <span class="shrink-0 text-xs font-semibold ${allDone ? "text-[#10b981]" : "text-gray-400"}">${gp.done}/${gp.total}</span>
                    </div>

                    <div class="flex items-center justify-between gap-3 border-b border-white/10 bg-black/25 px-4 py-2 text-xs text-gray-400">
                      <div class="h-1.5 max-w-[120px] flex-1 overflow-hidden rounded-full bg-white/10">
                        <div class="h-full rounded-full bg-[#10b981] transition-all duration-200" style="width:${gp.pct}%"></div>
                      </div>
                      <div class="flex items-center gap-1.5">
                        <button
                          type="button"
                          data-bulk-group="${escapeHtml(g.id)}"
                          data-bulk-state="1"
                          class="rounded-lg px-2 py-1 text-[11px] font-medium text-gray-300 hover:bg-white/10 hover:text-white"
                        >
                          Все
                        </button>
                        <button
                          type="button"
                          data-bulk-group="${escapeHtml(g.id)}"
                          data-bulk-state="0"
                          class="rounded-lg px-2 py-1 text-[11px] font-medium text-gray-400 hover:bg-white/10 hover:text-white"
                        >
                          Снять
                        </button>
                      </div>
                    </div>

                    <div class="group-body ${collapsed ? "is-collapsed" : ""} p-2">
                      <div class="flex flex-col gap-0.5">${rows}</div>
                    </div>
                  </div>
                `;
              })
              .join("");

            if (!groupsMarkup.trim()) return "";

            return `
              <section class="mt-6">
                <div class="mb-3">
                  <h2 class="text-lg font-bold text-white">${escapeHtml(act.title)}</h2>
                  ${act.subtitle ? `<p class="text-xs text-gray-400">${escapeHtml(act.subtitle)}</p>` : ""}
                </div>
                <div class="grid grid-cols-1 items-start gap-4 md:grid-cols-2">${groupsMarkup}</div>
              </section>
            `;
          })
          .join("");

        root.innerHTML = `
          <div class="mb-3">
            <button
              id="backCatalogBtn"
              type="button"
              class="rounded-xl border border-white/10 bg-[#191c24] px-3 py-1.5 text-xs font-medium text-gray-300 transition hover:bg-white/10 hover:text-white"
            >
              ← Все чек-листы
            </button>
          </div>

          <section class="rounded-2xl border border-white/10 bg-[#14161c] p-5 shadow-xl">
            <div class="flex flex-wrap items-start justify-between gap-4">
              <div>
                <div class="mb-1.5 flex flex-wrap gap-1.5">
                  <span class="rounded-full bg-[#e11d48]/15 px-2.5 py-0.5 text-[11px] font-semibold text-rose-300">${escapeHtml(cl.category || "Чек-лист")}</span>
                  ${cl.badge ? `<span class="rounded-full bg-[#f59e0b]/15 px-2.5 py-0.5 text-[11px] font-semibold text-amber-300">${escapeHtml(cl.badge)}</span>` : ""}
                </div>
                <h1 class="text-xl font-extrabold text-white sm:text-2xl">${escapeHtml(cl.title)}</h1>
                <p class="mt-1 text-xs text-gray-400 sm:text-sm">${escapeHtml(cl.subtitle || "")}</p>
              </div>

              <div class="flex flex-wrap gap-2">
                <button
                  id="expandGroupsBtn"
                  type="button"
                  class="rounded-xl border border-white/10 bg-[#191c24] px-3 py-1.5 text-xs font-medium text-gray-200 hover:bg-white/10"
                >
                  Развернуть все
                </button>
                <button
                  id="collapseGroupsBtn"
                  type="button"
                  class="rounded-xl border border-white/10 bg-[#191c24] px-3 py-1.5 text-xs font-medium text-gray-200 hover:bg-white/10"
                >
                  Свернуть все
                </button>
                <button
                  id="resetChecklistBtn"
                  type="button"
                  class="rounded-xl border border-red-500/30 bg-red-500/10 px-3 py-1.5 text-xs font-medium text-red-300 hover:bg-red-500/20"
                >
                  ${pendingResetConfirm ? "Нажми ещё раз для сброса" : "Сбросить прогресс"}
                </button>
              </div>
            </div>

            <div class="mt-4 border-t border-white/10 pt-4">
              <div class="mb-1.5 flex flex-wrap items-center justify-between gap-2 text-xs text-gray-300">
                <span>Всего по списку: <strong class="text-white">${clProg.done}</strong> / <strong class="text-white">${clProg.total}</strong> (${clProg.pct}%)</span>
                <span>Вкладка «${escapeHtml(activeTab.title)}»: <strong class="text-white">${tabProg.done}</strong> / <strong class="text-white">${tabProg.total}</strong> (${tabProg.pct}%)</span>
              </div>
              <div class="h-2.5 w-full overflow-hidden rounded-full bg-white/10">
                <div class="h-full rounded-full bg-gradient-to-r from-[#e11d48] via-[#f59e0b] to-[#10b981] transition-all duration-300" style="width:${clProg.pct}%"></div>
              </div>
            </div>
          </section>

          <div class="mt-4 flex flex-wrap gap-2">${tabButtons}</div>

          <div class="mt-4 flex flex-col gap-3 rounded-2xl border border-white/10 bg-[#14161c] p-3.5 sm:flex-row sm:items-center sm:justify-between">
            <input
              id="checklistSearch"
              type="search"
              value="${escapeHtml(checklistSearch)}"
              placeholder="Поиск по заданиям, коллекционкам и трофеям..."
              class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3.5 py-2 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none sm:max-w-md"
            />
            <div class="flex flex-wrap gap-1.5">
              <button type="button" data-filter-mode="all" class="rounded-xl border px-3 py-1.5 text-xs font-medium ${checklistFilter === "all" ? "border-white/25 bg-[#191c24] text-white" : "border-white/10 bg-[#0c0d10] text-gray-400 hover:text-white"}">Все</button>
              <button type="button" data-filter-mode="todo" class="rounded-xl border px-3 py-1.5 text-xs font-medium ${checklistFilter === "todo" ? "border-white/25 bg-[#191c24] text-white" : "border-white/10 bg-[#0c0d10] text-gray-400 hover:text-white"}">Не выполнено</button>
              <button type="button" data-filter-mode="done" class="rounded-xl border px-3 py-1.5 text-xs font-medium ${checklistFilter === "done" ? "border-white/25 bg-[#191c24] text-white" : "border-white/10 bg-[#0c0d10] text-gray-400 hover:text-white"}">Выполнено</button>
            </div>
          </div>

          ${
            actsMarkup.trim()
              ? actsMarkup
              : `<div class="mt-6 rounded-2xl border border-white/10 bg-[#14161c] p-8 text-center text-sm text-gray-400">По заданному фильтру или запросу ничего не найдено.</div>`
          }
        `;

        document.getElementById("backCatalogBtn").addEventListener("click", () => {
          state.route = { view: "catalog", checklistId: null, tabId: null, threadId: null };
          pendingResetConfirm = false;
          saveState();
          render();
        });

        root.querySelectorAll("[data-tab-btn]").forEach((btn) => {
          btn.addEventListener("click", () => {
            state.route.tabId = btn.getAttribute("data-tab-btn");
            pendingResetConfirm = false;
            saveState();
            render();
          });
        });

        const searchInput = document.getElementById("checklistSearch");
        if (searchInput) {
          searchInput.addEventListener("input", (e) => {
            checklistSearch = e.target.value;
            render();
            const nextEl = document.getElementById("checklistSearch");
            if (nextEl) {
              nextEl.focus();
              nextEl.setSelectionRange(nextEl.value.length, nextEl.value.length);
            }
          });
        }

        root.querySelectorAll("[data-filter-mode]").forEach((btn) => {
          btn.addEventListener("click", () => {
            checklistFilter = btn.getAttribute("data-filter-mode");
            render();
          });
        });

        root.querySelectorAll('input[type="checkbox"][data-check-group]').forEach((cb) => {
          cb.addEventListener("change", () => {
            const gId = cb.getAttribute("data-check-group");
            const idx = Number(cb.getAttribute("data-check-idx"));
            setItemChecked(cl.id, gId, idx, cb.checked);
            render();
          });
        });

        root.querySelectorAll("[data-toggle-group]").forEach((head) => {
          head.addEventListener("click", () => {
            const gId = head.getAttribute("data-toggle-group");
            state.collapsed[gId] = !state.collapsed[gId];
            saveState();
            render();
          });
        });

        root.querySelectorAll("[data-bulk-group]").forEach((btn) => {
          btn.addEventListener("click", (e) => {
            e.stopPropagation();
            const gId = btn.getAttribute("data-bulk-group");
            const val = btn.getAttribute("data-bulk-state") === "1";
            for (const act of activeTab.acts || []) {
              for (const g of act.groups || []) {
                if (g.id === gId) {
                  (g.items || []).forEach((_, i) => setItemChecked(cl.id, g.id, i, val));
                }
              }
            }
            render();
            showToast(val ? "Отмечены все пункты в группе" : "Отметки в группе сняты");
          });
        });

        document.getElementById("expandGroupsBtn").addEventListener("click", () => {
          for (const act of activeTab.acts || []) {
            for (const g of act.groups || []) {
              delete state.collapsed[g.id];
            }
          }
          saveState();
          render();
        });

        document.getElementById("collapseGroupsBtn").addEventListener("click", () => {
          for (const act of activeTab.acts || []) {
            for (const g of act.groups || []) {
              state.collapsed[g.id] = true;
            }
          }
          saveState();
          render();
        });

        document.getElementById("resetChecklistBtn").addEventListener("click", () => {
          if (!pendingResetConfirm) {
            pendingResetConfirm = true;
            render();
            clearTimeout(resetTimer);
            resetTimer = setTimeout(() => {
              pendingResetConfirm = false;
              render();
            }, 3500);
            return;
          }
          pendingResetConfirm = false;
          const prefix = `${cl.id}::`;
          Object.keys(state.checked).forEach((k) => {
            if (k.startsWith(prefix)) delete state.checked[k];
          });
          saveState();
          render();
          showToast("Прогресс по списку сброшен");
        });
      }

      // Экран форума (список тем и создание новой темы)
      function renderForum() {
        const root = document.getElementById("appRoot");
        const user = getCurrentUser();
        const q = forumSearch.trim().toLowerCase();

        const filteredThreads = (state.forumThreads || []).filter((t) => {
          const catOk = forumCategory === "Все" || t.category === forumCategory;
          const searchOk =
            !q ||
            String(t.title || "").toLowerCase().includes(q) ||
            String(t.body || "").toLowerCase().includes(q) ||
            String(t.authorName || "").toLowerCase().includes(q);
          return catOk && searchOk;
        });

        const sortedThreads = [...filteredThreads].sort((a, b) => {
          if (forumSort === "active") {
            const rDiff = (b.replies?.length || 0) - (a.replies?.length || 0);
            if (rDiff !== 0) return rDiff;
          }
          return new Date(b.createdAt).getTime() - new Date(a.createdAt).getTime();
        });

        const catTabs = ["Все", ...FORUM_CATEGORIES]
          .map((cat) => {
            const active = forumCategory === cat;
            return `
              <button
                type="button"
                data-forum-cat="${escapeHtml(cat)}"
                class="rounded-xl border px-3 py-1.5 text-xs font-semibold transition ${
                  active
                    ? "border-[#e11d48] bg-[#e11d48] text-white"
                    : "border-white/10 bg-[#14161c] text-gray-300 hover:border-white/25 hover:bg-[#191c24]"
                }"
              >
                ${escapeHtml(cat)}
              </button>
            `;
          })
          .join("");

        const threadCards = sortedThreads
          .map((t) => {
            const repCount = (t.replies || []).length;
            const isOwner = Boolean(user && (t.authorId === user.id || t.authorName === user.username));
            return `
              <article
                data-open-thread="${escapeHtml(t.id)}"
                class="cursor-pointer rounded-2xl border border-white/10 bg-[#14161c] p-5 transition hover:border-white/25 hover:bg-[#191c24]"
              >
                <div class="flex flex-wrap items-center justify-between gap-2">
                  <div class="flex flex-wrap items-center gap-2">
                    <span class="rounded-full bg-[#f59e0b]/15 px-2.5 py-0.5 text-[11px] font-semibold text-amber-300">
                      ${escapeHtml(t.category)}
                    </span>
                    <span class="text-xs font-medium text-gray-300">${escapeHtml(t.authorName)}</span>
                    <span class="text-xs text-gray-500">• ${escapeHtml(formatDateRu(t.createdAt))}</span>
                  </div>
                  <div class="flex items-center gap-2">
                    <span class="rounded-full bg-white/5 px-2.5 py-1 text-xs font-medium text-gray-300">
                      💬 ${repCount}
                    </span>
                    ${
                      isOwner
                        ? `<button type="button" data-delete-thread="${escapeHtml(t.id)}" class="rounded-lg border border-red-500/30 bg-red-500/10 px-2.5 py-1 text-[11px] font-medium text-red-300 hover:bg-red-500/20">Удалить</button>`
                        : ""
                    }
                  </div>
                </div>

                <h3 class="mt-2.5 text-lg font-bold text-white">${escapeHtml(t.title)}</h3>
                <p class="mt-1.5 line-clamp-2 text-sm text-gray-400">${escapeHtml(t.body)}</p>
              </article>
            `;
          })
          .join("");

        root.innerHTML = `
          <section class="rounded-2xl border border-white/10 bg-gradient-to-br from-[#e11d48]/15 via-[#14161c] to-[#f59e0b]/10 p-5 shadow-xl sm:p-6">
            <div class="flex flex-wrap items-start justify-between gap-4">
              <div>
                <h1 class="text-2xl font-extrabold text-white sm:text-3xl">Форум сообщества</h1>
                <p class="mt-1 text-sm text-gray-300">
                  Обсуждай прохождение, коллекционки, трофеи и предлагай новые игры для чек-листов.
                </p>
              </div>
              <div class="rounded-xl border border-white/10 bg-[#191c24] px-3.5 py-2 text-xs text-gray-300">
                Тем в разделе: <strong class="text-white">${sortedThreads.length}</strong>
              </div>
            </div>
          </section>

          <div class="mt-5 flex flex-wrap gap-2">${catTabs}</div>

          <div class="mt-4 flex flex-col gap-3 rounded-2xl border border-white/10 bg-[#14161c] p-3.5 sm:flex-row sm:items-center sm:justify-between">
            <input
              id="forumSearchInput"
              type="search"
              value="${escapeHtml(forumSearch)}"
              placeholder="Поиск по темам, сообщениям и авторам..."
              class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3.5 py-2 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none sm:max-w-md"
            />
            <div class="flex items-center gap-2">
              <span class="text-xs text-gray-400">Сортировка:</span>
              <select
                id="forumSortSelect"
                class="rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2 text-xs font-medium text-white focus:border-[#e11d48] focus:outline-none"
              >
                <option value="new" ${forumSort === "new" ? "selected" : ""}>Новые</option>
                <option value="active" ${forumSort === "active" ? "selected" : ""}>По активности</option>
              </select>
            </div>
          </div>

          <div class="mt-6 grid grid-cols-1 gap-6 lg:grid-cols-3">
            <div class="space-y-3 lg:col-span-2">
              ${
                threadCards.trim()
                  ? threadCards
                  : `<div class="rounded-2xl border border-white/10 bg-[#14161c] p-8 text-center text-sm text-gray-400">Тем по вашему запросу пока нет. Создайте первую!</div>`
              }
            </div>

            <div class="lg:col-span-1">
              <div class="sticky top-20 rounded-2xl border border-white/10 bg-[#14161c] p-5 shadow-lg">
                <h2 class="text-base font-bold text-white">Создать новую тему</h2>
                ${
                  user
                    ? `
                      <p class="mt-1 text-xs text-gray-400">Вы публикуете от имени <strong class="text-white">${escapeHtml(user.username)}</strong></p>
                      <form id="createThreadForm" class="mt-4 space-y-3">
                        <div>
                          <label for="threadTitleInput" class="mb-1 block text-xs font-medium text-gray-300">Заголовок темы</label>
                          <input
                            id="threadTitleInput"
                            type="text"
                            required
                            placeholder="Кратко опишите вопрос или тему"
                            class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none"
                          />
                        </div>
                        <div>
                          <label for="threadCategorySelect" class="mb-1 block text-xs font-medium text-gray-300">Категория</label>
                          <select
                            id="threadCategorySelect"
                            class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2 text-sm text-white focus:border-[#e11d48] focus:outline-none"
                          >
                            ${FORUM_CATEGORIES.map((c) => `<option value="${escapeHtml(c)}">${escapeHtml(c)}</option>`).join("")}
                          </select>
                        </div>
                        <div>
                          <label for="threadBodyInput" class="mb-1 block text-xs font-medium text-gray-300">Текст сообщения</label>
                          <textarea
                            id="threadBodyInput"
                            rows="5"
                            required
                            placeholder="Расскажите подробнее..."
                            class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none"
                          ></textarea>
                        </div>
                        <button
                          type="submit"
                          class="w-full rounded-xl bg-[#e11d48] py-2.5 text-xs font-semibold text-white transition hover:bg-rose-500"
                        >
                          Опубликовать тему
                        </button>
                      </form>
                    `
                    : `
                      <div class="mt-3 rounded-xl border border-[#f59e0b]/25 bg-[#f59e0b]/10 p-4 text-xs text-amber-100">
                        Чтобы создавать темы и оставлять ответы на форуме, войдите в аккаунт или зарегистрируйтесь.
                      </div>
                      <div class="mt-4 flex flex-col gap-2">
                        <button
                          id="forumPromptLoginBtn"
                          type="button"
                          class="w-full rounded-xl bg-[#e11d48] py-2.5 text-xs font-semibold text-white transition hover:bg-rose-500"
                        >
                          Войти в профиль
                        </button>
                        <button
                          id="forumPromptRegisterBtn"
                          type="button"
                          class="w-full rounded-xl border border-white/15 bg-[#191c24] py-2.5 text-xs font-semibold text-gray-200 transition hover:bg-white/10"
                        >
                          Зарегистрироваться
                        </button>
                      </div>
                    `
                }
              </div>
            </div>
          </div>
        `;

        root.querySelectorAll("[data-forum-cat]").forEach((btn) => {
          btn.addEventListener("click", () => {
            forumCategory = btn.getAttribute("data-forum-cat");
            render();
          });
        });

        const fSearch = document.getElementById("forumSearchInput");
        if (fSearch) {
          fSearch.addEventListener("input", (e) => {
            forumSearch = e.target.value;
            render();
            const nextEl = document.getElementById("forumSearchInput");
            if (nextEl) {
              nextEl.focus();
              nextEl.setSelectionRange(nextEl.value.length, nextEl.value.length);
            }
          });
        }

        const fSort = document.getElementById("forumSortSelect");
        if (fSort) {
          fSort.addEventListener("change", (e) => {
            forumSort = e.target.value;
            render();
          });
        }

        root.querySelectorAll("[data-open-thread]").forEach((card) => {
          card.addEventListener("click", () => {
            const tid = card.getAttribute("data-open-thread");
            state.route = { view: "thread", checklistId: null, tabId: null, threadId: tid };
            saveState();
            render();
            window.scrollTo({ top: 0, behavior: "smooth" });
          });
        });

        root.querySelectorAll("[data-delete-thread]").forEach((btn) => {
          btn.addEventListener("click", (e) => {
            e.stopPropagation();
            const tid = btn.getAttribute("data-delete-thread");
            state.forumThreads = state.forumThreads.filter((t) => t.id !== tid);
            saveState();
            render();
            showToast("Тема удалена");
          });
        });

        const createThreadForm = document.getElementById("createThreadForm");
        if (createThreadForm && user) {
          createThreadForm.addEventListener("submit", (e) => {
            e.preventDefault();
            const title = document.getElementById("threadTitleInput").value.trim();
            const category = document.getElementById("threadCategorySelect").value;
            const body = document.getElementById("threadBodyInput").value.trim();
            if (!title || !body) return;

            const newThread = {
              id: `thread-${Date.now().toString(36)}`,
              title,
              category,
              authorId: user.id,
              authorName: user.username,
              createdAt: new Date().toISOString(),
              body,
              replies: []
            };

            state.forumThreads.unshift(newThread);
            saveState();
            showToast("Тема опубликована на форуме!");
            state.route = { view: "thread", checklistId: null, tabId: null, threadId: newThread.id };
            render();
          });
        }

        const pLogin = document.getElementById("forumPromptLoginBtn");
        if (pLogin) pLogin.addEventListener("click", () => openAuthModal("login"));
        const pReg = document.getElementById("forumPromptRegisterBtn");
        if (pReg) pReg.addEventListener("click", () => openAuthModal("register"));
      }

      // Экран просмотра темы и ответов
      function renderThreadDetail() {
        const root = document.getElementById("appRoot");
        const user = getCurrentUser();
        const thread = (state.forumThreads || []).find((t) => t.id === state.route.threadId);

        if (!thread) {
          root.innerHTML = `
            <div class="rounded-2xl border border-white/10 bg-[#14161c] p-8 text-center">
              <p class="text-sm text-gray-300">Тема не найдена или была удалена.</p>
              <button id="backToForumMissingBtn" type="button" class="mt-4 rounded-xl bg-[#e11d48] px-4 py-2 text-xs font-semibold text-white">
                Вернуться на форум
              </button>
            </div>
          `;
          document.getElementById("backToForumMissingBtn").addEventListener("click", () => {
            state.route = { view: "forum", checklistId: null, tabId: null, threadId: null };
            saveState();
            render();
          });
          return;
        }

        const isThreadOwner = Boolean(user && (thread.authorId === user.id || thread.authorName === user.username));
        const replies = thread.replies || [];

        const repliesHtml = replies
          .map((r) => {
            const canDelete = Boolean(user && (r.authorId === user.id || r.authorName === user.username));
            return `
              <div class="rounded-2xl border border-white/10 bg-[#14161c] p-4">
                <div class="flex items-center justify-between gap-2">
                  <div class="flex items-center gap-2">
                    <div class="flex h-7 w-7 items-center justify-center rounded-full bg-[#191c24] text-[11px] font-bold text-rose-300 border border-white/10">
                      ${escapeHtml(getInitials(r.authorName))}
                    </div>
                    <span class="text-xs font-semibold text-white">${escapeHtml(r.authorName)}</span>
                    <span class="text-[11px] text-gray-500">• ${escapeHtml(formatDateRu(r.createdAt))}</span>
                  </div>
                  ${
                    canDelete
                      ? `<button type="button" data-delete-reply="${escapeHtml(r.id)}" class="rounded-lg border border-red-500/30 bg-red-500/10 px-2 py-1 text-[11px] font-medium text-red-300 hover:bg-red-500/20">Удалить</button>`
                      : ""
                  }
                </div>
                <p class="mt-2.5 whitespace-pre-line text-sm leading-relaxed text-gray-200">${escapeHtml(r.text)}</p>
              </div>
            `;
          })
          .join("");

        root.innerHTML = `
          <div class="mb-4 flex flex-wrap items-center justify-between gap-2">
            <button
              id="backForumBtn"
              type="button"
              class="rounded-xl border border-white/10 bg-[#191c24] px-3 py-1.5 text-xs font-medium text-gray-300 transition hover:bg-white/10 hover:text-white"
            >
              ← Назад к списку тем
            </button>
            ${
              isThreadOwner
                ? `<button id="deleteCurrentThreadBtn" type="button" class="rounded-xl border border-red-500/30 bg-red-500/10 px-3 py-1.5 text-xs font-medium text-red-300 hover:bg-red-500/20">Удалить тему</button>`
                : ""
            }
          </div>

          <article class="rounded-2xl border border-white/10 bg-[#14161c] p-5 shadow-xl sm:p-6">
            <div class="flex flex-wrap items-center gap-2">
              <span class="rounded-full bg-[#f59e0b]/15 px-2.5 py-0.5 text-[11px] font-semibold text-amber-300">${escapeHtml(thread.category)}</span>
              <span class="text-xs font-semibold text-white">${escapeHtml(thread.authorName)}</span>
              <span class="text-xs text-gray-500">• ${escapeHtml(formatDateRu(thread.createdAt))}</span>
            </div>
            <h1 class="mt-3 text-xl font-extrabold text-white sm:text-2xl">${escapeHtml(thread.title)}</h1>
            <p class="mt-3 whitespace-pre-line text-sm leading-relaxed text-gray-200">${escapeHtml(thread.body)}</p>
          </article>

          <div class="mt-6">
            <h2 class="mb-3 text-base font-bold text-white">Ответы (${replies.length})</h2>
            <div class="space-y-3">
              ${
                repliesHtml.trim()
                  ? repliesHtml
                  : `<div class="rounded-2xl border border-white/10 bg-[#14161c] p-6 text-center text-xs text-gray-400">Ответов пока нет. Напишите первый!</div>`
              }
            </div>
          </div>

          <div class="mt-6 rounded-2xl border border-white/10 bg-[#14161c] p-5">
            <h3 class="text-sm font-bold text-white">Добавить ответ</h3>
            ${
              user
                ? `
                  <form id="replyForm" class="mt-3 space-y-3">
                    <textarea
                      id="replyTextInput"
                      rows="3"
                      required
                      placeholder="Напишите свой ответ от имени ${escapeHtml(user.username)}..."
                      class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3.5 py-2.5 text-sm text-white placeholder-gray-500 focus:border-[#e11d48] focus:outline-none"
                    ></textarea>
                    <button
                      type="submit"
                      class="rounded-xl bg-[#e11d48] px-4 py-2 text-xs font-semibold text-white transition hover:bg-rose-500"
                    >
                      Отправить ответ
                    </button>
                  </form>
                `
                : `
                  <p class="mt-1.5 text-xs text-gray-400">Войдите или зарегистрируйтесь, чтобы оставить комментарий в этой теме.</p>
                  <button
                    id="threadAuthBtn"
                    type="button"
                    class="mt-3 rounded-xl bg-[#e11d48] px-4 py-2 text-xs font-semibold text-white transition hover:bg-rose-500"
                  >
                    Войти / Зарегистрироваться
                  </button>
                `
            }
          </div>
        `;

        document.getElementById("backForumBtn").addEventListener("click", () => {
          state.route = { view: "forum", checklistId: null, tabId: null, threadId: null };
          saveState();
          render();
        });

        const delThreadBtn = document.getElementById("deleteCurrentThreadBtn");
        if (delThreadBtn) {
          delThreadBtn.addEventListener("click", () => {
            state.forumThreads = state.forumThreads.filter((t) => t.id !== thread.id);
            state.route = { view: "forum", checklistId: null, tabId: null, threadId: null };
            saveState();
            render();
            showToast("Тема удалена");
          });
        }

        root.querySelectorAll("[data-delete-reply]").forEach((btn) => {
          btn.addEventListener("click", () => {
            const rid = btn.getAttribute("data-delete-reply");
            thread.replies = (thread.replies || []).filter((r) => r.id !== rid);
            saveState();
            render();
            showToast("Ответ удалён");
          });
        });

        const replyForm = document.getElementById("replyForm");
        if (replyForm && user) {
          replyForm.addEventListener("submit", (e) => {
            e.preventDefault();
            const text = document.getElementById("replyTextInput").value.trim();
            if (!text) return;
            thread.replies = thread.replies || [];
            thread.replies.push({
              id: `rep-${Date.now().toString(36)}`,
              authorId: user.id,
              authorName: user.username,
              createdAt: new Date().toISOString(),
              text
            });
            saveState();
            render();
            showToast("Ответ добавлен");
          });
        }

        const tAuthBtn = document.getElementById("threadAuthBtn");
        if (tAuthBtn) tAuthBtn.addEventListener("click", () => openAuthModal("login"));
      }

      // Экран профиля пользователя
      function renderProfile() {
        const root = document.getElementById("appRoot");
        const user = getCurrentUser();

        if (!user) {
          root.innerHTML = `
            <section class="mx-auto max-w-xl rounded-2xl border border-white/10 bg-[#14161c] p-6 text-center shadow-xl">
              <div class="mx-auto flex h-14 w-14 items-center justify-center rounded-2xl bg-[#191c24] text-xl font-extrabold text-amber-300 border border-white/10">
                ?
              </div>
              <h1 class="mt-4 text-2xl font-extrabold text-white">Вы ещё не вошли в профиль</h1>
              <p class="mt-2 text-sm text-gray-400">
                Войдите в существующий аккаунт, зарегистрируйте новый или создайте быстрый демо-профиль, чтобы редактировать имя и описание, видеть статистику и участвовать на форуме.
              </p>
              <div class="mt-5 flex flex-wrap justify-center gap-2.5">
                <button
                  id="profileOpenLoginBtn"
                  type="button"
                  class="rounded-xl bg-[#e11d48] px-5 py-2.5 text-xs font-semibold text-white transition hover:bg-rose-500"
                >
                  Войти
                </button>
                <button
                  id="profileOpenRegBtn"
                  type="button"
                  class="rounded-xl border border-white/15 bg-[#191c24] px-5 py-2.5 text-xs font-semibold text-white transition hover:bg-white/10"
                >
                  Регистрация
                </button>
              </div>
            </section>
          `;
          document.getElementById("profileOpenLoginBtn").addEventListener("click", () => openAuthModal("login"));
          document.getElementById("profileOpenRegBtn").addEventListener("click", () => openAuthModal("register"));
          return;
        }

        const lists = allChecklists();
        let totalItems = 0;
        let doneItems = 0;
        const perChecklistHtml = lists
          .map((cl) => {
            const p = getChecklistProgress(cl);
            totalItems += p.total;
            doneItems += p.done;
            return `
              <div class="rounded-xl border border-white/10 bg-[#191c24] p-3.5">
                <div class="flex items-center justify-between gap-2 text-xs">
                  <span class="font-semibold text-white">${escapeHtml(cl.title)}</span>
                  <span class="font-bold text-[#10b981]">${p.pct}%</span>
                </div>
                <div class="mt-1.5 text-[11px] text-gray-400">${p.done} из ${p.total} пунктов выполнено</div>
                <div class="mt-2 h-1.5 w-full overflow-hidden rounded-full bg-white/10">
                  <div class="h-full rounded-full bg-[#10b981]" style="width:${p.pct}%"></div>
                </div>
              </div>
            `;
          })
          .join("");

        const overallPct = totalItems ? Math.round((doneItems / totalItems) * 100) : 0;
        const forumStats = getUserForumStats(user);

        root.innerHTML = `
          <section class="rounded-2xl border border-white/10 bg-[#14161c] p-5 shadow-xl sm:p-6">
            <div class="flex flex-wrap items-start justify-between gap-4">
              <div class="flex items-center gap-4">
                <div class="flex h-16 w-16 shrink-0 items-center justify-center rounded-2xl bg-gradient-to-br from-[#e11d48] to-[#f59e0b] text-xl font-extrabold text-white shadow-lg">
                  ${escapeHtml(getInitials(user.username))}
                </div>
                <div>
                  <h1 class="text-2xl font-extrabold text-white">${escapeHtml(user.username)}</h1>
                  <div class="mt-0.5 flex flex-wrap items-center gap-2 text-xs text-gray-400">
                    <span>${escapeHtml(user.handle)}</span>
                    ${
                      user.provider === "google"
                        ? `<span class="rounded-full border border-sky-400/30 bg-sky-400/10 px-2 py-0.5 text-[10px] font-semibold text-sky-300">Google</span>`
                        : ""
                    }
                    <span>•</span>
                    <span>На сайте с ${escapeHtml(formatDateRu(user.joinedAt))}</span>
                  </div>
                  <p class="mt-2 max-w-xl text-sm text-gray-300">${escapeHtml(user.bio || "")}</p>
                </div>
              </div>

              <button
                id="logoutBtn"
                type="button"
                class="rounded-xl border border-red-500/30 bg-red-500/10 px-4 py-2 text-xs font-semibold text-red-300 transition hover:bg-red-500/20"
              >
                Выйти из профиля
              </button>
            </div>

            <div class="mt-6 grid grid-cols-1 gap-3 sm:grid-cols-3">
              <div class="rounded-2xl border border-white/10 bg-[#191c24] p-4">
                <div class="text-xs text-gray-400">Общий прогресс чек-листов</div>
                <div class="mt-1 text-2xl font-extrabold text-white">${overallPct}%</div>
                <div class="mt-0.5 text-xs text-gray-500">${doneItems} из ${totalItems} пунктов</div>
              </div>
              <div class="rounded-2xl border border-white/10 bg-[#191c24] p-4">
                <div class="text-xs text-gray-400">Создано тем на форуме</div>
                <div class="mt-1 text-2xl font-extrabold text-amber-300">${forumStats.threadsCount}</div>
                <div class="mt-0.5 text-xs text-gray-500">Активные обсуждения</div>
              </div>
              <div class="rounded-2xl border border-white/10 bg-[#191c24] p-4">
                <div class="text-xs text-gray-400">Ответов на форуме</div>
                <div class="mt-1 text-2xl font-extrabold text-[#10b981]">${forumStats.repliesCount}</div>
                <div class="mt-0.5 text-xs text-gray-500">Комментариев в ветках</div>
              </div>
            </div>
          </section>

          <div class="mt-6 grid grid-cols-1 gap-6 lg:grid-cols-2">
            <section class="rounded-2xl border border-white/10 bg-[#14161c] p-5">
              <h2 class="text-base font-bold text-white">Редактировать профиль</h2>
              <form id="editProfileForm" class="mt-4 space-y-3">
                <div>
                  <label for="editUsernameInput" class="mb-1 block text-xs font-medium text-gray-300">Отображаемое имя</label>
                  <input
                    id="editUsernameInput"
                    type="text"
                    required
                    value="${escapeHtml(user.username)}"
                    class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2 text-sm text-white focus:border-[#e11d48] focus:outline-none"
                  />
                </div>
                <div>
                  <label for="editBioInput" class="mb-1 block text-xs font-medium text-gray-300">О себе / статус</label>
                  <textarea
                    id="editBioInput"
                    rows="3"
                    placeholder="Расскажите о любимых играх или целях по платине..."
                    class="w-full rounded-xl border border-white/10 bg-[#0c0d10] px-3 py-2 text-sm text-white focus:border-[#e11d48] focus:outline-none"
                  >${escapeHtml(user.bio || "")}</textarea>
                </div>
                <button
                  type="submit"
                  class="rounded-xl bg-[#e11d48] px-4 py-2 text-xs font-semibold text-white transition hover:bg-rose-500"
                >
                  Сохранить изменения
                </button>
              </form>
            </section>

            <section class="rounded-2xl border border-white/10 bg-[#14161c] p-5">
              <h2 class="text-base font-bold text-white">Прогресс по чек-листам</h2>
              <div class="mt-4 space-y-3">${perChecklistHtml}</div>
            </section>
          </div>
        `;

        document.getElementById("logoutBtn").addEventListener("click", () => {
          state.currentUserId = null;
          saveState();
          showToast("Вы вышли из профиля");
          render();
        });

        document.getElementById("editProfileForm").addEventListener("submit", (e) => {
          e.preventDefault();
          const nextName = document.getElementById("editUsernameInput").value.trim();
          const nextBio = document.getElementById("editBioInput").value.trim();
          if (nextName.length < 2 || nextName.length > 24) {
            showToast("Имя должно быть от 2 до 24 символов");
            return;
          }
          user.username = nextName;
          user.bio = nextBio;
          saveState();
          render();
          showToast("Профиль обновлён");
        });
      }

      // Главный рендер
      function render() {
        syncStorageIndicator();
        syncAuthHeader();
        const view = state.route.view;
        if (view === "checklist" && state.route.checklistId) {
          renderChecklist();
        } else if (view === "forum") {
          renderForum();
        } else if (view === "thread") {
          renderThreadDetail();
        } else if (view === "profile") {
          renderProfile();
        } else {
          renderCatalog();
        }
      }

      // Модалка создания своего чек-листа
      const modal = document.getElementById("createModal");
      const form = document.getElementById("createChecklistForm");

      function openCreateModal() {
        modal.classList.remove("hidden");
        modal.classList.add("flex");
        document.getElementById("customTitleInput").focus();
      }

      function closeCreateModal() {
        modal.classList.add("hidden");
        modal.classList.remove("flex");
      }

      document.getElementById("closeCreateModalBtn").addEventListener("click", closeCreateModal);
      document.getElementById("cancelCreateModalBtn").addEventListener("click", closeCreateModal);
      modal.addEventListener("click", (e) => {
        if (e.target === modal) closeCreateModal();
      });

      form.addEventListener("submit", (e) => {
        e.preventDefault();
        const title = document.getElementById("customTitleInput").value.trim();
        const category = document.getElementById("customCategoryInput").value.trim() || "Свой список";
        const groupTitle = document.getElementById("customGroupInput").value.trim() || "Основной список";
        const lines = document
          .getElementById("customItemsTextarea")
          .value.split(/\r?\n/)
          .map((s) => s.trim())
          .filter(Boolean);

        if (!title || lines.length === 0) return;

        const id = `custom-${Date.now().toString(36)}`;
        state.customChecklists.push({
          id,
          title,
          subtitle: `Пользовательский чек-лист (${lines.length} пунктов)`,
          badge: "Свой список",
          category,
          tabs: [
            {
              id: `${id}-tab-1`,
              title: "Основной",
              acts: [
                {
                  id: `${id}-act-1`,
                  title,
                  groups: [{ id: `${id}-g-1`, title: groupTitle, items: lines }]
                }
              ]
            }
          ]
        });
        saveState();
        closeCreateModal();
        form.reset();
        openChecklist(id);
        showToast("Чек-лист создан");
      });

      // Навигация шапки и экспорт/импорт JSON
      document.getElementById("homeBrandBtn").addEventListener("click", () => {
        state.route = { view: "catalog", checklistId: null, tabId: null, threadId: null };
        pendingResetConfirm = false;
        saveState();
        render();
      });

      document.getElementById("navCatalogBtn").addEventListener("click", () => {
        state.route = { view: "catalog", checklistId: null, tabId: null, threadId: null };
        pendingResetConfirm = false;
        saveState();
        render();
      });

      document.getElementById("navForumBtn").addEventListener("click", () => {
        state.route = { view: "forum", checklistId: null, tabId: null, threadId: null };
        pendingResetConfirm = false;
        saveState();
        render();
      });

      document.getElementById("profileAuthPillBtn").addEventListener("click", () => {
        if (getCurrentUser()) {
          state.route = { view: "profile", checklistId: null, tabId: null, threadId: null };
          saveState();
          render();
        } else {
          openAuthModal("login");
        }
      });

      document.getElementById("exportJsonBtn").addEventListener("click", () => {
        try {
          const data = JSON.stringify({ exportedAt: new Date().toISOString(), state }, null, 2);
          const blob = new Blob([data], { type: "application/json" });
          const url = URL.createObjectURL(blob);
          const a = document.createElement("a");
          a.href = url;
          a.download = `checklist-hub-${new Date().toISOString().slice(0, 10)}.json`;
          document.body.appendChild(a);
          a.click();
          a.remove();
          URL.revokeObjectURL(url);
          showToast("Бэкап сохранён в JSON");
        } catch (err) {
          showToast("Не удалось выгрузить JSON");
        }
      });

      const fileInput = document.getElementById("importFileInput");
      document.getElementById("importJsonBtn").addEventListener("click", () => fileInput.click());
      fileInput.addEventListener("change", (e) => {
        const file = e.target.files && e.target.files[0];
        if (!file) return;
        const reader = new FileReader();
        reader.onload = () => {
          try {
            const parsed = JSON.parse(String(reader.result || "{}"));
            const incoming = parsed.state && typeof parsed.state === "object" ? parsed.state : parsed;
            if (incoming.checked && typeof incoming.checked === "object") state.checked = incoming.checked;
            if (incoming.collapsed && typeof incoming.collapsed === "object") state.collapsed = incoming.collapsed;
            if (Array.isArray(incoming.customChecklists)) state.customChecklists = incoming.customChecklists;
            if (Array.isArray(incoming.users)) state.users = incoming.users;
            if (typeof incoming.currentUserId === "string" || incoming.currentUserId === null) {
              state.currentUserId = incoming.currentUserId;
            }
            if (Array.isArray(incoming.forumThreads) && incoming.forumThreads.length > 0) {
              state.forumThreads = incoming.forumThreads;
            }
            saveState();
            render();
            showToast("Данные импортированы из JSON");
          } catch (err) {
            showToast("Ошибка чтения JSON-файла");
          }
          fileInput.value = "";
        };
        reader.readAsText(file);
      });

      render();
    })();
  </script>
</body>
</html>

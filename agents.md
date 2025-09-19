* asynchronous agents
  * are tools that independently perform tasks in a code repository: they clone the project, create branches, make changes, and open PRs for review. The developer remains in the decision-making loop but doesn't need to supervise every step in real-time (HITL)."
  * HITL - human in the loop
* programs
* OpenAI Codex (ChatGPT)
  * uruchamiasz bezpośrednio z czatu — agent ładuje repo do odizolowanego środowiska (sandbox/cloud env), wykonuje komendy, uruchamia testy i finalnie otwiera PR. Nie reaguje natywnie na zdarzenia z GitHuba (działa “pull-based” od rozmowy), ale nadrabia jakością rozumowania i szybkością iteracji w zadaniach ad-hoc. Dobrze sprawdza się przy krótkich przebiegach (1–30 min), refaktoryzacjach przekrojowych i dopisywaniu testów, o ile repo ma stabilne CI. Najlepsze efekty daje z jasnymi artefaktami (AGENTS.md, plan testów, checklisty), które ograniczają “dryf” planu. Słabiej wypada w długich, wieloetapowych migracjach i tam, gdzie wymagane są workflowy sterowane eventami repo.
  * Gdy już korzystasz z ChatGPT Plus i chcesz dodać agenta bez nowej subskrypcji - dostajesz czat + agenta w jednym
  * Gdy zależy Ci na jakości rozumowania/kodu i uruchamiasz zadania ad-hoc (1–30 min) z poziomu przeglądarki
  * Gdy pracujesz poza pełnym ekosystemem GitHuba (np. GitLab z mirrorem do PR) i potrzebujesz uniwersalnego narzędzia
  * Jako narzędzie uzupełniające do szybkiego prototypowania, zanim zadanie wejdzie w formalny PR-flow 
* Google Jules jest „GitHub-first”:
  * reaguje na etykiety/komentarze w issue, generuje plan do akceptacji (HITL) i przeprowadza zmiany z pełnym logiem kroków. Świetnie nadaje się do seryjnych prac utrzymaniowych (aktualizacje zależności, dopisywanie testów, repo hygiene) oraz refaktoryzacji rozłożonych na wiele plików. Ma wbudowane limity i kolejki z retry/backoff, więc przewidywalnie rozkłada obciążenie na wiele zadań dziennie. Interfejs klarownie pokazuje postęp i pozwala łatwo wracać do historii działań agenta. Ograniczeniem bywa praca poza GitHubem lub bardzo duże migracje, które trzeba dzielić na mniejsze, zatwierdzane partie.
  * Gdy działasz solo/freelance i wystarczy darmowe ~15 zadań/dzień (Intro) do higieny repo i drobnych usprawnień
  * Gdy mały zespół na GitHubie chce automatyzować powtarzalne prace (Pro: ~100 zadań/dzień, większa równoległość)
  * Gdy potrzebujesz zatwierdzać plan przed zmianami i chcesz widzieć logi działań w UI
  * Gdy chcesz cyklicznie prowadzić refaktoryzacje i aktualizacje w wielu plikach (branch+PR out-of-the-box)
* GitHub Copilot Agent Mode
  * działa natywnie w ekosystemie GitHuba, dzięki czemu respektuje branch protection, wykorzystuje znane zasoby (Actions) i zostawia pełny ślad audytowy w PR/Actions. Potrafi reagować na przypisanie issue czy komentarze w PR, iterując zmiany w tym samym wątku, co upraszcza governance i przegląd. Dla organizacji to naturalny wybór: SSO/SAML, polityki organizacyjne i zgodność z procesami bezpieczeństwa “po prostu działają”. Minusem jest ścisła zależność od GitHuba (czasem jeden aktywny job na repo) i koszt wykonywania pracy przez Actions. Najmocniej błyszczy w zespołach enterprise, które chcą minimum nowych narzędzi i maksimum kontroli w jednym miejscu.
  * Gdy cała organizacja pracuje na GitHubie i wymagasz pełnego audytu w PR/Actions oraz respektowania branch protection
  * Gdy chcesz wyzwalać agenta przez przypisanie issue lub komentarz w PR i iterować zmianami w tym samym PR
  * Gdy priorytetem jest governance (uprawnienia, SSO/SAML, polityki organizacji) bez dodatkowych narzędzi poza GitHubem
  * Gdy chcesz, by działania agenta zużywały znane zasoby (minuty Actions) i były widoczne w standardowych logach
* Devin 
  * to „cięższa artyleria”: pełne środowisko (shell, edytor, przeglądarka), długie sesje i integracje z narzędziami zadaniowymi (Slack/Linear/Jira), co ułatwia prowadzenie złożonych migracji. Sprawdza się, gdy trzeba łączyć analizę, implementację i debug w jednym autonomicznym przebiegu, a wynik ma skończyć jako PR. Oferuje rozbudowane UI do obserwacji, metryki/rozliczanie (np. jednostki ACU) i opcje enterprise/self-host, co bywa atutem w większych organizacjach. Wymaga jednak dobrze przygotowanego repo (testy, CI, dane przykładowe) oraz budżetu adekwatnego do dłuższych i bardziej zasobożernych zadań. Do prostych, powtarzalnych prac może być nadmiarowy — lepsze ROI dają lżejsze agenty PR-owe.
  * Gdy prowadzisz duże migracje/refaktoryzacje i potrzebujesz autonomicznego środowiska (shell+edytor+browser) z integracjami taskowymi
  * Gdy budżet i skala backlogu uzasadniają koszt SaaS (od ~$500/mies. za zespół) oraz chcesz rozważyć wariant Enterprise/self-host
  * Gdy komunikacja przez Slack/Linear/Jira ma inicjować sesje i chcesz śledzić postęp w dedykowanym UI/IDE
  * Jako narzędzie uzupełniające do ciężkich zadań (migracje, CI fixes) obok lżejszych agentów PR-owych     

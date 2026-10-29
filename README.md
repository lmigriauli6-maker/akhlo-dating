# akhlo-dating

<!DOCTYPE html>
<html lang="ka">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#100b16">
  <meta name="description" content="ახლო — გაიცანი საინტერესო ადამიანები საქართველოში.">
  <title>ახლო — Akhlo Dating</title>
  <style>
    :root {
      --bg: #100b16;
      --panel: #1b1424;
      --pink: #ff4f91;
      --purple: #a875ff;
      --text: #fff8ff;
      --muted: #b6a9c2;
      --gold: #eac58b;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      min-height: 100vh;
      background: radial-gradient(ellipse at top, #35203e 0, var(--bg) 52%);
      color: var(--text);
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }
    button { font: inherit; cursor: pointer; }
    .app { max-width: 480px; min-height: 100vh; margin: auto; padding: 20px 16px 100px; }
    header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 24px; }
    .brand { font-size: 30px; font-weight: 850; letter-spacing: -1px; }
    .brand span { color: var(--pink); }
    .premium {
      color: #241608; background: linear-gradient(135deg, #ffe5ad, #d5a65e);
      border: 0; border-radius: 999px; padding: 10px 13px; font-weight: 800;
    }
    .intro { margin-bottom: 20px; }
    .intro h1 { font-size: 27px; margin: 0 0 7px; }
    .intro p { margin: 0; color: var(--muted); font-size: 14px; }
    .filters { display: flex; gap: 8px; overflow-x: auto; margin-bottom: 18px; }
    .filter { white-space: nowrap; border: 1px solid #45334f; border-radius: 999px; padding: 9px 14px; background: #1b1424; color: var(--muted); }
    .filter.active { background: var(--pink); border-color: var(--pink); color: white; }
    .profile {
      overflow: hidden; position: relative; border-radius: 26px;
      border: 1px solid #49334e; background: var(--panel);
      box-shadow: 0 18px 55px #0006;
    }
    .portrait {
      min-height: 330px; display: flex; flex-direction: column; justify-content: flex-end;
      padding: 22px; background:
        linear-gradient(0deg, #100b16 0%, #100b1630 50%, #100b1600 100%),
        linear-gradient(135deg, #57305e, #bd668a 48%, #f0b6a0);
    }
    .portrait .emoji { font-size: 100px; text-align: center; filter: drop-shadow(0 8px 18px #0005); }
    .portrait .demo { align-self: flex-start; font-size: 11px; letter-spacing: 1px; color: #fff; background: #0006; padding: 7px 10px; border-radius: 999px; margin-bottom: 12px; }
    .person h2 { margin: 0 0 6px; font-size: 27px; }
    .person p { margin: 0; color: #e7dce9; font-size: 14px; }
    .bio { padding: 16px 18px 4px; color: #d4c6dc; line-height: 1.5; font-size: 14px; }
    .tags { display: flex; flex-wrap: wrap; gap: 7px; padding: 12px 18px 18px; }
    .tag { background: #30223b; border: 1px solid #4a3556; border-radius: 999px; padding: 7px 10px; color: #e9d9f3; font-size: 12px; }
    .actions { display: flex; justify-content: center; gap: 18px; padding: 20px 0; }
    .action {
      width: 62px; height: 62px; border-radius: 50%; border: 1px solid #49334e;
      background: #21172b; color: white; font-size: 27px;
      box-shadow: 0 8px 22px #0004;
    }
    .action.like { background: linear-gradient(135deg, #ff4f91, #b23dca); border: 0; }
    .action.star { color: #f4ce8b; }
    .message { min-height: 22px; text-align: center; color: #ffc0da; font-size: 13px; }
    .section { display: none; padding: 18px; border: 1px solid #49334e; border-radius: 22px; background: #1b1424; }
    .section h2 { margin-top: 0; }
    .section p { color: var(--muted); line-height: 1.6; }
    .bottom {
      position: fixed; bottom: 0; left: 50%; transform: translateX(-50%);
      width: min(480px, 100%); display: flex; justify-content: space-around;
      padding: 12px 6px calc(12px + env(safe-area-inset-bottom));
      background: #130d1bee; backdrop-filter: blur(16px);
      border-top: 1px solid #382742; z-index: 5;
    }
    .nav { border: 0; background: transparent; color: #9e90aa; font-size: 11px; display: grid; gap: 5px; justify-items: center; }
    .nav b { font-size: 21px; font-weight: 500; }
    .nav.active { color: var(--pink); }
    .primary { border: 0; border-radius: 13px; background: linear-gradient(135deg, var(--pink), var(--purple)); color: white; padding: 12px 16px; font-weight: 750; }
    @media (max-width: 360px) { .portrait { min-height: 290px; } .intro h1 { font-size: 24px; } }
  </style>
</head>
<body>
  <main class="app">
    <header>
      <div class="brand">ახლო<span>.</span></div>
      <button class="premium" id="premiumBtn">✦ PREMIUM</button>
    </header>

    <section id="discoverView">
      <div class="intro">
        <h1>შენი შემდეგი ისტორია ✨</h1>
        <p>ახალი ნაცნობობები შეიძლება აქ დაიწყოს.</p>
      </div>
      <div class="filters">
        <button class="filter active">ყველა</button>
        <button class="filter">ახლოს</button>
        <button class="filter">ახალი</button>
        <button class="filter">ონლაინ</button>
      </div>
      <article class="profile">
        <div class="portrait">
          <div class="emoji" id="personEmoji">🌸</div>
          <div class="demo">DEMO PROFILE</div>
          <div class="person">
            <h2 id="personName">ანა, 24</h2>
            <p id="personLocation">📍 თბილისი · მაგალითი პროფილი</p>
          </div>
        </div>
        <div class="bio" id="personBio">მიყვარს მოგზაურობა, კარგი მუსიკა და ახალი ადგილების აღმოჩენა.</div>
        <div class="tags" id="personTags">
          <span class="tag">მოგზაურობა</span><span class="tag">მუსიკა</span><span class="tag">ყავა</span>
        </div>
      </article>
      <div class="actions">
        <button class="action" id="passBtn" aria-label="გამოტოვება">✕</button>
        <button class="action star" id="starBtn" aria-label="რჩეულებში დამატება">★</button>
        <button class="action like" id="likeBtn" aria-label="მოწონება">♥</button>
      </div>
      <div class="message" id="message" aria-live="polite"></div>
    </section>

    <section class="section" id="matchesView">
      <h2>შენი მოწონებები 💗</h2>
      <p id="likesText">ჯერ არავინ მოგიწონებია. დაათვალიერე პროფილები და მონიშნე ის, ვინც მოგწონს.</p>
    </section>

    <section class="section" id="chatView">
      <h2>შეტყობინებები 💬</h2>
      <p>ჩატი ჯერ დემო ვერსიაშია. რეალური შეტყობინებებისთვის მოგვიანებით დავაკავშირებთ ანგარიშებსა და მონაცემთა ბაზას.</p>
    </section>

    <section class="section" id="profileView">
      <h2>ჩემი პროფილი 👤</h2>
      <p>აქ დაემატება რეგისტრაცია, ფოტო, ბიოგრაფია და პარამეტრები.</p>
      <button class="primary" id="editProfileBtn">პროფილის შექმნა</button>
      <p id="profileMessage"></p>
    </section>
  </main>

  <nav class="bottom" aria-label="მთავარი მენიუ">
    <button class="nav active" data-view="discover"><b>♡</b>გაცნობა</button>
    <button class="nav" data-view="matches"><b>♥</b>მოწონებები</button>
    <button class="nav" data-view="chat"><b>▢</b>ჩატი</button>
    <button class="nav" data-view="profile"><b>♙</b>პროფილი</button>
  </nav>

  <script>
    const people = [
      { name: "ანა, 24", location: "📍 თბილისი · მაგალითი პროფილი", emoji: "🌸", bio: "მიყვარს მოგზაურობა, კარგი მუსიკა და ახალი ადგილების აღმოჩენა.", tags: ["მოგზაურობა", "მუსიკა", "ყავა"] },
      { name: "ნინი, 23", location: "📍 რუსთავი · მაგალითი პროფილი", emoji: "🌷", bio: "თავისუფალ დროს ვკითხულობ, ვსეირნობ და ახალ კაფეებს ვეძებ.", tags: ["წიგნები", "სეირნობა", "კაფეები"] },
      { name: "მარიამი, 25", location: "📍 თბილისი · მაგალითი პროფილი", emoji: "🦋", bio: "მიყვარს ბუნება, კინო და გულწრფელი საუბრები.", tags: ["ბუნება", "კინო", "მეგობრობა"] }
    ];
    let current = 0;
    const liked = [];
    const $ = id => document.getElementById(id);

    function renderPerson() {
      const p = people[current];
      $("personName").textContent = p.name;
      $("personLocation").textContent = p.location;
      $("personEmoji").textContent = p.emoji;
      $("personBio").textContent = p.bio;
      $("personTags").replaceChildren(...p.tags.map(tag => {
        const el = document.createElement("span");
        el.className = "tag";
        el.textContent = tag;
        return el;
      }));
      $("message").textContent = "";
    }
    function nextPerson() {
      current = (current + 1) % people.length;
      renderPerson();
    }
    $("passBtn").addEventListener("click", () => {
      $("message").textContent = "პროფილი გამოტოვებულია";
      nextPerson();
    });
    $("likeBtn").addEventListener("click", () => {
      const name = people[current].name;
      if (!liked.includes(name)) liked.push(name);
      $("likesText").textContent = "შენ მოიწონე: " + liked.join(", ");
      $("message").textContent = "მოწონება შენახულია ამ დემო სესიაში 💗";
      nextPerson();
    });
    $("starBtn").addEventListener("click", () => {
      $("message").textContent = "რჩეულებში მონიშნულია ★";
    });
    $("premiumBtn").addEventListener("click", () => {
      alert("ახლო Premium მალე დაემატება. გადახდები ჯერ ჩართული არ არის.");
    });
    $("editProfileBtn").addEventListener("click", () => {
      $("profileMessage").textContent = "რეგისტრაციასა და პროფილის შენახვას შემდეგ ეტაპზე დავამატებთ.";
    });
    document.querySelectorAll(".filter").forEach(button => {
      button.addEventListener("click", () => {
        document.querySelectorAll(".filter").forEach(b => b.classList.remove("active"));
        button.classList.add("active");
      });
    });
    const views = ["discover", "matches", "chat", "profile"];
    document.querySelectorAll(".nav").forEach(button => {
      button.addEventListener("click", () => {
        const target = button.dataset.view;
        views.forEach(view => {
          const section = $(view + "View");
          section.style.display = view === target ? (view === "discover" ? "block" : "block") : "none";
        });
        document.querySelectorAll(".nav").forEach(b => b.classList.toggle("active", b === button));
      });
    });
    renderPerson();
  </script>
</body>
</html>

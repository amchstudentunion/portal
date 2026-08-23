<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Students' Union | Medical College Portal</title>
  
  <!-- Minimalist Editorial Typography -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">

  <style>
    :root {
      --bg: #FBFBFA;
      --surface: #FFFFFF;
      --text: #181818;
      --muted: #737373;
      --border: #E5E5E3;
      --font-serif: 'Cormorant Garamond', Georgia, serif;
      --font-sans: 'Inter', -apple-system, sans-serif;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { background: var(--bg); color: var(--text); font-family: var(--font-sans); line-height: 1.6; padding: 2rem 5vw; }
    
    header { border-bottom: 1px solid var(--border); padding-bottom: 2rem; margin-bottom: 4rem; }
    nav { display: flex; justify-content: space-between; align-items: baseline; flex-wrap: wrap; gap: 1rem; }
    .brand { font-family: var(--font-serif); font-size: 1.75rem; text-decoration: none; color: var(--text); font-weight: 600; letter-spacing: -0.01em; }
    .nav-links a { margin-left: 1.5rem; text-decoration: none; color: var(--muted); font-size: 0.85rem; text-transform: uppercase; letter-spacing: 0.05em; transition: color 0.2s; }
    .nav-links a:hover { color: var(--text); }

    .hero { margin-bottom: 6rem; max-width: 900px; }
    .hero h1 { font-family: var(--font-serif); font-size: clamp(3rem, 7vw, 5.5rem); font-weight: 400; line-height: 1.05; letter-spacing: -0.02em; margin-bottom: 1.5rem; }
    .hero p { font-size: 1.15rem; color: var(--muted); font-weight: 300; max-width: 640px; }

    section { margin-bottom: 6rem; }
    .section-header { display: flex; justify-content: space-between; align-items: baseline; border-bottom: 1px solid var(--border); padding-bottom: 0.75rem; margin-bottom: 2rem; }
    .section-header h2 { font-family: var(--font-serif); font-size: 2.25rem; font-weight: 400; margin: 0; }
    .section-header span { font-size: 0.8rem; text-transform: uppercase; letter-spacing: 0.05em; color: var(--muted); }

    .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 1.5rem; }
    .card { border: 1px solid var(--border); padding: 1.5rem; background: var(--surface); }
    .card h3 { font-family: var(--font-serif); font-size: 1.4rem; margin-bottom: 0.5rem; font-weight: 400; }
    .card p { color: var(--muted); font-size: 0.88rem; margin-bottom: 1rem; }
    .card a { text-decoration: none; color: var(--text); font-weight: 500; font-size: 0.85rem; border-bottom: 1px solid var(--text); }

    /* Batch selector cards */
    .batches-list { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1rem; }
    .batch-btn {
      border: 1px solid var(--border);
      padding: 1.5rem 1.25rem;
      background: var(--surface);
      text-align: left;
      cursor: pointer;
      transition: all 0.2s ease;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      min-height: 130px;
    }
    .batch-btn:hover { border-color: var(--text); background: #f4f4f2; }
    .batch-btn .badge { font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.05em; color: var(--muted); }
    .batch-btn .title { font-family: var(--font-serif); font-size: 1.6rem; color: var(--text); margin-top: 0.5rem; line-height: 1.1; }
    .batch-btn.crmi { border: 1.5px solid var(--text); }

    /* Google Map Responsive Wrapper */
    .google-map-container {
      position: relative;
      width: 100%;
      height: 480px;
      border: 1px solid var(--border);
      background: var(--surface);
      overflow: hidden;
    }
    .google-map-container iframe {
      width: 100%;
      height: 100%;
      border: 0;
      filter: grayscale(15%) contrast(1.02);
    }

    /* Batch Dossier Modal Window */
    .modal-backdrop {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(24, 24, 24, 0.6);
      backdrop-filter: blur(4px);
      z-index: 9999;
      overflow-y: auto;
      padding: 3rem 1.5rem;
    }
    .modal-container {
      max-width: 860px;
      margin: 0 auto;
      background: var(--bg);
      border: 1px solid var(--border);
      padding: clamp(1.5rem, 5vw, 3.5rem);
      position: relative;
      animation: modalFadeIn 0.25s ease-out;
    }
    @keyframes modalFadeIn {
      from { opacity: 0; transform: translateY(15px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .close-btn {
      position: absolute;
      top: 1.5rem;
      right: 1.5rem;
      background: none;
      border: 1px solid var(--border);
      padding: 0.4rem 0.8rem;
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      cursor: pointer;
      color: var(--text);
    }
    .close-btn:hover { background: var(--text); color: var(--bg); }

    .dossier-flag-banner {
      border: 1px solid var(--border);
      background: var(--surface);
      padding: 2.5rem 2rem;
      text-align: center;
      margin: 1.5rem 0 2.5rem 0;
      position: relative;
    }
    .dossier-flag-banner::before {
      content: "FLAG & INSIGNIA";
      position: absolute;
      top: 0.6rem;
      left: 0.8rem;
      font-size: 0.65rem;
      letter-spacing: 0.08em;
      color: var(--muted);
    }
    .flag-symbol { font-size: 3rem; margin-bottom: 0.5rem; display: block; }
    .batch-dossier-title { font-family: var(--font-serif); font-size: clamp(2.5rem, 5vw, 4rem); font-weight: 400; line-height: 1; margin-bottom: 0.5rem; }
    .batch-motto { font-family: var(--font-serif); font-style: italic; font-size: 1.35rem; color: var(--muted); margin-bottom: 1.5rem; }
    
    .gallery-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 1rem; margin-top: 1.5rem; }
    .gallery-placeholder {
      aspect-ratio: 4/3;
      background: #EEE;
      border: 1px dashed var(--border);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 1rem;
      text-align: center;
      font-size: 0.8rem;
      color: var(--muted);
    }

    table { width: 100%; border-collapse: collapse; font-size: 0.9rem; text-align: left; }
    th { padding: 0.75rem 0; font-weight: 400; border-bottom: 1px solid var(--text); font-family: var(--font-serif); font-size: 1.1rem; }
    td { padding: 1rem 0; border-bottom: 1px solid var(--border); }

    footer { border-top: 1px solid var(--border); padding-top: 2rem; color: var(--muted); font-size: 0.85rem; display: flex; justify-content: space-between; flex-wrap: wrap; gap: 1rem; }
  </style>
</head>
<body>

  <header>
    <nav>
      <a href="#" class="brand">STUDENTS' UNION</a>
      <div class="nav-links">
        <a href="#batches">Batches</a>
        <a href="#map-section">Field Map</a>
        <a href="#sos">Night SOS</a>
        <a href="#exchange">Exchange</a>
        <a href="#clinical-notes">Clinical Guide</a>
        <a href="#grievance">Drop-Box</a>
      </div>
    </nav>
  </header>

  <main>
    <!-- Hero Manifesto -->
    <section class="hero">
      <h1>Autonomy, camaraderie, and student welfare.</h1>
      <p>The collective portal for life within hospital wards and Tiruvannamalai town. Dedicated to orienting freshers and celebrating the heritage of all five MBBS batches.</p>
    </section>

    <!-- Batches Section -->
    <section id="batches">
      <div class="section-header">
        <h2>Batches of MBBS</h2>
        <span>Select Batch to Open Space</span>
      </div>
      <div class="batches-list">
        <div class="batch-btn crmi" onclick="openBatchSpace('trigarianz')">
          <span class="badge">Seniormost / CRMI</span>
          <span class="title">Trigarianz &rarr;</span>
        </div>
        <div class="batch-btn" onclick="openBatchSpace('ryzentronz')">
          <span class="badge">Final Year MBBS</span>
          <span class="title">Ryzentronz &rarr;</span>
        </div>
        <div class="batch-btn" onclick="openBatchSpace('xandarianz')">
          <span class="badge">Third Year MBBS</span>
          <span class="title">Xandarianz &rarr;</span>
        </div>
        <div class="batch-btn" onclick="openBatchSpace('stratonz')">
          <span class="badge">Second Year MBBS</span>
          <span class="title">Stratonz &rarr;</span>
        </div>
        <div class="batch-btn" onclick="openBatchSpace('zenarianz')">
          <span class="badge">First Year / Freshers</span>
          <span class="title">Zenarianz &rarr;</span>
        </div>
      </div>
    </section>

    <!-- Google Map Integration Section -->
    <section id="map-section">
      <div class="section-header">
        <h2>Tiruvannamalai Student Navigator</h2>
        <span>Google Maps Integration</span>
      </div>
      
      <div class="google-map-container">
        <!-- Live Google Map Embed Centered on Medical College & Town Area -->
        <iframe 
          src="https://maps.google.com/maps?q=Government%20Medical%20College%20and%20Hospital%20Thiruvannamalai&t=&z=13&ie=UTF8&iwloc=&output=embed" 
          allowfullscreen="" 
          loading="lazy" 
          referrerpolicy="no-referrer-when-downgrade">
        </iframe>
      </div>

      <!-- Quick Location Links -->
      <div class="grid" style="margin-top: 2rem;">
        <div class="card">
          <h3>Medical Hubs & Campus</h3>
          <p>GMC & Hospital Master Plan Complex, Arunai Medical College (Velu Nagar), and Collectorate Complex.</p>
          <a href="https://maps.google.com/?q=Government+Medical+College+and+Hospital+Thiruvannamalai" target="_blank" rel="noopener">Open GMC in Google Maps &rarr;</a>
        </div>
        <div class="card">
          <h3>Food & Cafes</h3>
          <p>Dharshan Dhaba (Bypass), Toppi Vappa Biryani, and Ocolate Cafe for team dinners and late parcels.</p>
          <a href="https://maps.google.com/?q=Dharshan+Dhaba+Tiruvannamalai" target="_blank" rel="noopener">Get Directions to Dhaba &rarr;</a>
        </div>
        <div class="card">
          <h3>Sports & Retail</h3>
          <p>SDAT Stadium / District Sports Complex on Collectorate Road, Yousta (Polur Road) for clothing basics.</p>
          <a href="https://maps.google.com/?q=SDAT+Stadium+Tiruvannamalai" target="_blank" rel="noopener">View SDAT Stadium &rarr;</a>
        </div>
      </div>
    </section>

    <!-- Night Postings SOS -->
    <section id="sos">
      <div class="section-header">
        <h2>Night Postings SOS Guide</h2>
        <span>Emergency & Duty Support</span>
      </div>
      <div class="grid">
        <div class="card">
          <h3>Gate Autos (24/7)</h3>
          <ul style="list-style: none; font-size: 0.9rem; line-height: 2;">
            <li style="display: flex; justify-content: space-between; border-bottom: 1px dashed var(--border);">
              <span>Hospital Gate Auto Stand</span>
              <a href="tel:+919876543210" style="color: var(--text); font-weight: 500;">Call Direct</a>
            </li>
            <li style="display: flex; justify-content: space-between;">
              <span>Old Bus Stand Night Shift</span>
              <a href="tel:+919876543212" style="color: var(--text); font-weight: 500;">Call Direct</a>
            </li>
          </ul>
        </div>

        <div class="card">
          <h3>Late Deliveries & Meals</h3>
          <ul style="list-style: none; font-size: 0.9rem; line-height: 2;">
            <li style="display: flex; justify-content: space-between; border-bottom: 1px dashed var(--border);">
              <span>Campus Night Tea Stall</span>
              <span style="color: var(--muted);">Intercom #402</span>
            </li>
            <li style="display: flex; justify-content: space-between;">
              <span>Dharshan Dhaba / Toppi Vappa</span>
              <span style="color: var(--muted);">Late Parcel Available</span>
            </li>
          </ul>
        </div>

        <div class="card">
          <h3>24-Hour Pharmacies</h3>
          <ul style="list-style: none; font-size: 0.9rem; line-height: 2;">
            <li style="display: flex; justify-content: space-between; border-bottom: 1px dashed var(--border);">
              <span>Govt Hospital In-House Meds</span>
              <span style="color: var(--muted);">OPD Ground Floor</span>
            </li>
            <li style="display: flex; justify-content: space-between;">
              <span>Arunai Medical College Meds</span>
              <span style="color: var(--muted);">Velu Nagar Hub</span>
            </li>
          </ul>
        </div>
      </div>
    </section>

    <!-- Senior-Junior Book & Equipment Exchange -->
    <section id="exchange">
      <div class="section-header">
        <h2>Senior–Junior Exchange</h2>
        <span>Peer Classifieds</span>
      </div>
      <table>
        <thead>
          <tr>
            <th>Item Description</th>
            <th>Category</th>
            <th>Offered By</th>
            <th>Price / Terms</th>
            <th style="text-align: right;">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Full Osteology Bone Set (Original, Grade A)</td>
            <td style="color: var(--muted);">Anatomy Kit</td>
            <td>Xandarianz</td>
            <td>₹4,500 (Fixed)</td>
            <td style="text-align: right;"><a href="#" style="color: var(--text); text-decoration: underline;">Request Item</a></td>
          </tr>
          <tr>
            <td>B.D. Chaurasia (Vol 1-4, Latest Edition)</td>
            <td style="color: var(--muted);">Textbook</td>
            <td>Ryzentronz</td>
            <td>Free Pass-Down</td>
            <td style="text-align: right;"><a href="#" style="color: var(--text); text-decoration: underline;">Request Item</a></td>
          </tr>
          <tr>
            <td>Clinical Kit: Knee Hammer, Tuning Fork (128/512Hz)</td>
            <td style="color: var(--muted);">Diagnostics</td>
            <td>Trigarianz</td>
            <td>₹600</td>
            <td style="text-align: right;"><a href="#" style="color: var(--text); text-decoration: underline;">Request Item</a></td>
          </tr>
        </tbody>
      </table>
    </section>

    <!-- Clinical Posting Survival Notes -->
    <section id="clinical-notes">
      <div class="section-header">
        <h2>Clinical Survival Protocols</h2>
        <span>Fresher Reference</span>
      </div>
      <div class="grid">
        <div class="card">
          <h3>1. OPD Postings Decorum</h3>
          <ul style="font-size: 0.85rem; color: var(--text); padding-left: 1.2rem; line-height: 1.8;">
            <li>Clean, ironed white apron with college ID pinned on the left chest.</li>
            <li>Mandatory kit: Stethoscope, pen torch, measuring tape, knee hammer, diary.</li>
            <li>Report to the assigned unit PG by 08:45 AM for ward allocations.</li>
          </ul>
        </div>
        <div class="card">
          <h3>2. Case Sheet Structure</h3>
          <ol style="font-size: 0.85rem; color: var(--text); padding-left: 1.2rem; line-height: 1.8;">
            <li><strong>Demographics:</strong> Name, Age, Sex, Occupation, Native place.</li>
            <li><strong>Chief Complaints:</strong> In chronological order with duration.</li>
            <li><strong>HOPI:</strong> History of Present Illness with negative history.</li>
            <li><strong>Systemic Exam:</strong> Inspection &rarr; Palpation &rarr; Percussion &rarr; Auscultation.</li>
          </ol>
        </div>
      </div>
    </section>

    <!-- Anonymous Grievance Drop-Box -->
    <section id="grievance">
      <div class="section-header">
        <h2>Anonymous Union Drop-Box</h2>
        <span>Zero-Trace Redressal</span>
      </div>
      <div class="card" style="max-width: 700px;">
        <p style="font-size: 0.9rem; color: var(--muted); margin-bottom: 1.5rem;">
          Submissions are fully anonymous and contain zero user tracking. Use this form for mess complaints, hostel repairs, library issues, or academic concerns.
        </p>
        <form style="display: flex; flex-direction: column; gap: 1.25rem;">
          <div>
            <label style="display: block; font-size: 0.8rem; text-transform: uppercase; letter-spacing: 0.05em; margin-bottom: 0.4rem;">Category</label>
            <select required style="width: 100%; padding: 0.75rem; border: 1px solid var(--border); background: var(--bg); font-family: var(--font-sans); font-size: 0.9rem;">
              <option value="mess">Mess & Dining Quality</option>
              <option value="hostel">Hostel Infrastructure / Water / Electrical</option>
              <option value="academic">Academic & Posting Schedules</option>
              <option value="library">Library Facilities</option>
              <option value="welfare">General Student Welfare</option>
            </select>
          </div>
          <div>
            <label style="display: block; font-size: 0.8rem; text-transform: uppercase; letter-spacing: 0.05em; margin-bottom: 0.4rem;">Batch Context</label>
            <select style="width: 100%; padding: 0.75rem; border: 1px solid var(--border); background: var(--bg); font-family: var(--font-sans); font-size: 0.9rem;">
              <option value="undisclosed">Prefer not to say</option>
              <option value="zenarianz">Zenarianz (Freshers)</option>
              <option value="stratonz">Stratonz</option>
              <option value="xandarianz">Xandarianz</option>
              <option value="ryzentronz">Ryzentronz</option>
              <option value="trigarianz">Trigarianz (CRMI)</option>
            </select>
          </div>
          <div>
            <label style="display: block; font-size: 0.8rem; text-transform: uppercase; letter-spacing: 0.05em; margin-bottom: 0.4rem;">Concern / Resolution Needed</label>
            <textarea rows="4" required placeholder="State facts, location, and specific resolution requested..." style="width: 100%; padding: 0.75rem; border: 1px solid var(--border); background: var(--bg); font-family: var(--font-sans); font-size: 0.9rem; resize: vertical;"></textarea>
          </div>
          <button type="submit" style="background: var(--text); color: var(--bg); border: none; padding: 0.85rem 2rem; font-family: var(--font-serif); font-size: 1.1rem; cursor: pointer; align-self: flex-start;">
            Submit Anonymous Dispatch &rarr;
          </button>
        </form>
      </div>
    </section>
  </main>

  <footer>
    <p>&copy; Students' Union. Independent & Student-Run.</p>
    <p>Tiruvannamalai, Tamil Nadu</p>
  </footer>

  <!-- Dedicated Batch Dossier Modal -->
  <div id="batchModal" class="modal-backdrop" onclick="closeBatchModal(event)">
    <div class="modal-container" onclick="event.stopPropagation()">
      <button class="close-btn" onclick="closeBatchModalDirect()">Close &times;</button>
      <div id="batchDossierContent"></div>
    </div>
  </div>

  <script>
    const batchData = {
      trigarianz: {
        name: "TRIGARIANZ",
        yearBadge: "Compulsory Rotatory Medical Internship (CRMI) — Seniormost Batch",
        flagImg: "assets/trigarianz/flag.png",
        flagSymbol: "⚔️ ⚕️",
        flagDesign: "The Obsidian Standard // Gold Caduceus on Jet Field",
        motto: "“Through the crucible of duty, we master the healing arts.”",
        manifesto: "The seniormost vanguard of the student body. Currently managing Casualty, Surgery, Medicine, and Rural rotations across the Master Plan Complex. Guardians of traditions, mentors of clinical instincts.",
        council: [
          { role: "Batch Representative (Men)", name: "Dr. [Name Placeholder]" },
          { role: "Batch Representative (Women)", name: "Dr. [Name Placeholder]" },
          { role: "Intern Academic Secretary", name: "Dr. [Name Placeholder]" },
          { role: "Clinical Duty Liaison", name: "Dr. [Name Placeholder]" }
        ],
        milestones: [
          "100% Clinical Ward Rotations across GMC Tiruvannamalai",
          "Inter-College Symposium Organizers & Clinical Champions",
          "Founding stewards of the Student Welfare Forum"
        ],
        gallery: [
          { url: "assets/trigarianz/photo-1.jpg", caption: "Casualty Night Duty Shift", alt: "Trigarianz casualty posting team" },
          { url: "assets/trigarianz/photo-2.jpg", caption: "Annual Inter-Batch Cricket Finalists", alt: "Cricket tournament champions" }
        ]
      },
      ryzentronz: {
        name: "RYZENTRONZ",
        yearBadge: "Final Professional MBBS (Part I & II)",
        flagImg: "",
        flagSymbol: "⚡ 🦅",
        flagDesign: "The Crimson Crest // Ascending Phoenix & Stethoscope",
        motto: "“Unyielding precision, unshakeable solidarity.”",
        manifesto: "Mastering Medicine, Surgery, OBG, and Paediatrics. The senior council driving academic peer-teaching and steering college delegations across national medical conferences.",
        council: [
          { role: "General Secretary", name: "[Name Placeholder]" },
          { role: "Academic Coordinator", name: "[Name Placeholder]" },
          { role: "Cultural & Sports Secretary", name: "[Name Placeholder]" }
        ],
        milestones: [
          "State-level Quiz Finalists (TN-MGRMU)",
          "Lead Coordinators for the Annual Blood Donation Drive",
          "Pioneers of the Centralized Logbook Assistance Initiative"
        ],
        gallery: [
          { url: "assets/ryzentronz/photo-1.jpg", caption: "Ward Postings Case Rounds", alt: "Ward rounds" },
          { url: "assets/ryzentronz/photo-2.jpg", caption: "National Med-Conference Delegation", alt: "Conference delegates" }
        ]
      },
      xandarianz: {
        name: "XANDARIANZ",
        yearBadge: "Third Year Professional MBBS",
        flagImg: "",
        flagSymbol: "🛡️ ⚔️",
        flagDesign: "The Cobalt Seal // Shield of Diagnostics & Scalpel",
        motto: "“From pathology to therapeutics, our insight sharpens.”",
        manifesto: "Deep in the trenches of Ophthalmology, ENT, and Community Medicine. Anchoring the core of inter-batch sports, literary societies, and campus initiatives.",
        council: [
          { role: "Batch Representative", name: "[Name Placeholder]" },
          { role: "Sports Captain", name: "[Name Placeholder]" }
        ],
        milestones: [
          "Field Health Survey Coordinators in Chengam block",
          "Winners of Inter-batch Football & Badminton League"
        ],
        gallery: [
          { url: "assets/xandarianz/photo-1.jpg", caption: "Community Medicine Village Survey", alt: "Field survey" }
        ]
      },
      stratonz: {
        name: "STRATONZ",
        yearBadge: "Second Year Professional MBBS",
        flagImg: "",
        flagSymbol: "🏹 🏛️",
        flagDesign: "The Bronze Banner // Pillar of Knowledge & Arrow",
        motto: "“Decoding diseases, defending human vitality.”",
        manifesto: "Navigating Pathology, Microbiology, and Pharmacology while bridging the transition from basic preclinical sciences to hospital bedside clinics.",
        council: [
          { role: "Batch Lead", name: "[Name Placeholder]" },
          { role: "Lab & Library Liaison", name: "[Name Placeholder]" }
        ],
        milestones: [
          "Founding members of the Preclinical Journal Club",
          "Hospital Orientation Leads for Zenarianz"
        ],
        gallery: [
          { url: "assets/stratonz/photo-1.jpg", caption: "Histopathology Practical Sessions", alt: "Microbiology lab" }
        ]
      },
      zenarianz: {
        name: "ZENARIANZ",
        yearBadge: "First Professional MBBS — Welcoming Freshers",
        flagImg: "",
        flagSymbol: "🌱 🌟",
        flagDesign: "The Emerald Pennant // The Dawn Star & Lotus",
        motto: "“The journey begins with curiosity, courage, and compassion.”",
        manifesto: "The newest members of the medical fraternity in Tiruvannamalai. Beginning the rigorous passage through Anatomy dissection halls, Physiology practicals, and Biochemistry cycles.",
        council: [
          { role: "Fresher Class Representative (Men)", name: "[TBD / Election Pending]" },
          { role: "Fresher Class Representative (Women)", name: "[TBD / Election Pending]" }
        ],
        milestones: [
          "Induction and White Coat Ceremony Milestone",
          "Inaugural Girivalam Batch Walkway Assembly"
        ],
        gallery: [
          { url: "assets/zenarianz/photo-1.jpg", caption: "White Coat Ceremony", alt: "White coat ceremony" }
        ]
      }
    };

    function openBatchSpace(batchKey) {
      const data = batchData[batchKey];
      if (!data) return;

      const html = `
        <span style="font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.08em; color: var(--muted);">${data.yearBadge}</span>
        <h1 class="batch-dossier-title">${data.name}</h1>
        <p class="batch-motto">${data.motto}</p>

        <div class="dossier-flag-banner">
          ${data.flagImg 
            ? `<img src="${data.flagImg}" alt="${data.name} Flag" style="max-height: 90px; margin-bottom: 0.75rem; display: inline-block;" onerror="this.style.display='none'"/>` 
            : `<span class="flag-symbol">${data.flagSymbol}</span>`
          }
          <strong style="font-family: var(--font-serif); font-size: 1.25rem; display: block; margin-bottom: 0.25rem;">${data.flagDesign}</strong>
          <span style="font-size: 0.8rem; color: var(--muted);">Official Batch Standard & Insignia</span>
        </div>

        <h3 style="font-family: var(--font-serif); font-size: 1.5rem; font-weight: 400; margin-bottom: 0.5rem; border-bottom: 1px solid var(--border); padding-bottom: 0.4rem;">
          Batch Manifesto
        </h3>
        <p style="font-size: 0.95rem; color: #333; margin-bottom: 2rem; line-height: 1.7;">
          ${data.manifesto}
        </p>

        <h3 style="font-family: var(--font-serif); font-size: 1.5rem; font-weight: 400; margin-bottom: 0.5rem; border-bottom: 1px solid var(--border); padding-bottom: 0.4rem;">
          Batch Council & Representatives
        </h3>
        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 1rem; margin-bottom: 2.5rem;">
          ${data.council.map(c => `
            <div style="border: 1px solid var(--border); padding: 1rem; background: var(--surface);">
              <span style="display: block; font-size: 0.72rem; text-transform: uppercase; color: var(--muted); letter-spacing: 0.05em; margin-bottom: 0.25rem;">
                ${c.role}
              </span>
              <strong style="font-family: var(--font-serif); font-size: 1.15rem; color: var(--text);">
                ${c.name}
              </strong>
            </div>
          `).join('')}
        </div>

        <h3 style="font-family: var(--font-serif); font-size: 1.5rem; font-weight: 400; margin-bottom: 0.5rem; border-bottom: 1px solid var(--border); padding-bottom: 0.4rem;">
          Batch Milestones
        </h3>
        <ul style="font-size: 0.9rem; padding-left: 1.2rem; line-height: 1.8; margin-bottom: 2.5rem;">
          ${data.milestones.map(m => `<li>${m}</li>`).join('')}
        </ul>

        <h3 style="font-family: var(--font-serif); font-size: 1.5rem; font-weight: 400; margin-bottom: 0.5rem; border-bottom: 1px solid var(--border); padding-bottom: 0.4rem;">
          Batch Gallery & Photographic Archive
        </h3>
        <div class="gallery-grid">
          ${data.gallery.map(img => `
            <div style="border: 1px solid var(--border); background: var(--surface); padding: 0.5rem;">
              <div style="aspect-ratio: 4/3; overflow: hidden; background: #eee; position: relative;">
                <img 
                  src="${img.url}" 
                  alt="${img.alt}" 
                  style="width: 100%; height: 100%; object-fit: cover; display: block;"
                  onerror="this.parentElement.innerHTML='<div class=\\'gallery-placeholder\\'><span>📷 Photo pending</span></div>'"
                />
              </div>
              <span style="display: block; font-size: 0.8rem; color: var(--muted); padding: 0.5rem 0.25rem 0.25rem 0.25rem;">
                ${img.caption}
              </span>
            </div>
          `).join('')}
        </div>
      `;

      document.getElementById('batchDossierContent').innerHTML = html;
      document.getElementById('batchModal').style.display = 'block';
      document.body.style.overflow = 'hidden';
    }

    function closeBatchModal(e) {
      if (e.target.id === 'batchModal') closeBatchModalDirect();
    }

    function closeBatchModalDirect() {
      document.getElementById('batchModal').style.display = 'none';
      document.body.style.overflow = 'auto';
    }

    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') closeBatchModalDirect();
    });
  </script>
</body>
</html>

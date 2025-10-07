# ⚖️ Justice Seek AI – Accountability Console

**Educational prototype for ethical AI legal workflow with human-in-the-loop approval and audit trails**

> ⚠️ **Educational Use Only**: This is a demonstration prototype for law school educational purposes. Not for production legal work.

## 📋 Overview

Justice Seek AI Accountability Console is a clickable prototype demonstrating how AI-assisted legal workflows can incorporate:

- ✅ **Human-in-the-loop approval** - No AI-generated content goes out without attorney review
- 📊 **Transparent audit trails** - Every action logged in immutable ledger
- 🎨 **ADHD-friendly UI** - Clean, organized interface with visual hierarchy
- 🛡️ **Compliance panels** - Built-in risk scoring and ethical guardrails

## 🏗️ Architecture

```
/dashboard    → overview + active drafts
/case/:id     → preview + approval modal
/ledger       → immutable audit history
/settings     → user roles, compliance toggles
```

## 🎯 Key Features

### 1. Dashboard
- Pending approvals table with case overview
- Risk scores (0-100 scale)
- Quick actions: Preview, Approve, Edit
- Real-time status tracking

### 2. Draft Preview Modal
- Full document preview
- Comment/feedback system
- Approve and sign workflow
- Version control

### 3. Immutable Audit Ledger
- Timestamp logs
- User attribution
- Action history
- Compliance verification

### 4. Settings Panel
```yaml
review_settings:
  require_human_approval: true
  liability_filter: enabled
  tone_analyzer_threshold: 0.20
  remediation_first_default: true
  bar_verification_required: true

notifications:
  email_to: aaron@example.com
  slack_channel: "#justice-seek-ai"

storage:
  ledger_backend: Notion_DB
  backup: Google_Drive
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- npm or yarn
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/aaj2127/justice-seek-ai-accountability-console.git

# Navigate to project directory
cd justice-seek-ai-accountability-console

# Install dependencies
npm install

# Start development server
npm run dev
```

### Project Structure

```
justice-seek-ai-accountability-console/
├── src/
│   ├── components/
│   │   ├── Dashboard.jsx
│   │   ├── PreviewModal.jsx
│   │   ├── AuditLedger.jsx
│   │   └── Settings.jsx
│   ├── App.jsx
│   └── main.jsx
├── public/
├── package.json
├── vite.config.js
├── tailwind.config.js
└── README.md
```

## 💻 Component Specifications

### Dashboard Component

```jsx
export default function Dashboard() {
  return (
    <main className="p-6 space-y-6 bg-slate-50 min-h-screen">
      <header className="flex justify-between items-center">
        <h1 className="text-2xl font-bold">Justice Seek AI Dashboard</h1>
        <button className="px-4 py-2 bg-blue-600 text-white rounded-xl">
          + New Draft
        </button>
      </header>

      <section>
        <h2 className="text-lg font-semibold mb-2">Pending Approvals</h2>
        <table className="w-full bg-white shadow rounded-2xl">
          <thead className="text-left bg-gray-100">
            <tr>
              <th className="p-3">Case ID</th>
              <th className="p-3">Domain</th>
              <th className="p-3">Document</th>
              <th className="p-3">Risk Score</th>
              <th className="p-3">Status</th>
              <th className="p-3 text-right">Actions</th>
            </tr>
          </thead>
          <tbody>
            {["JS-00123","JS-00124"].map((id)=>(
              <tr key={id} className="border-t hover:bg-gray-50">
                <td className="p-3">{id}</td>
                <td className="p-3">placeholder-domain.com</td>
                <td className="p-3">Outreach Letter</td>
                <td className="p-3 text-green-700">98 / 100</td>
                <td className="p-3">Awaiting Review</td>
                <td className="p-3 text-right space-x-2">
                  <button className="text-blue-600 underline">Preview</button>
                  <button className="text-green-600 underline">Approve</button>
                  <button className="text-amber-600 underline">Edit</button>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </section>
    </main>
  )
}
```

### Preview Modal Component

```jsx
function PreviewModal({caseID}) {
 return (
  <dialog open className="rounded-2xl p-6 max-w-3xl bg-white shadow-2xl">
   <h2 className="text-xl font-semibold mb-2">Draft Preview – {caseID}</h2>
   <article className="prose max-h-[60vh] overflow-y-auto mb-4">
     <p><strong>Subject:</strong> Accessibility Review Notice – &lt;domain&gt;</p>
     <p>Dear &lt;Compliance Officer&gt;, …</p>
   </article>
   <div className="flex justify-between items-center">
     <label className="text-sm text-gray-500">
       Comment (visible to AI editor)
     </label>
     <textarea className="w-full border rounded p-2" rows="3"
       placeholder="Add feedback before approval…" />
   </div>
   <div className="flex justify-end gap-3 mt-4">
     <button className="px-4 py-2 rounded-lg border">Cancel</button>
     <button className="px-4 py-2 bg-green-600 text-white rounded-lg">
       Approve and Sign
     </button>
   </div>
  </dialog>
 )
}
```

### Audit Ledger Component

```jsx
function AuditLedger() {
  const entries = [
    { timestamp: "2025-10-07 11:45", user: "AI Paralegal", action: "Draft Created", caseID: "JS-00123", notes: "ADA template generated" },
    { timestamp: "2025-10-07 11:46", user: "Compliance Bot", action: "Risk Scan", caseID: "JS-00123", notes: "Score 98 (Clean)" },
    { timestamp: "— Pending —", user: "Aaron Johnson", action: "Human Review", caseID: "JS-00123", notes: "Awaiting signature" }
  ];

  return (
    <div className="p-6">
      <h2 className="text-2xl font-bold mb-4">Immutable Audit Ledger</h2>
      <table className="w-full bg-white shadow rounded-xl">
        <thead className="bg-gray-100">
          <tr>
            <th className="p-3 text-left">Timestamp</th>
            <th className="p-3 text-left">User</th>
            <th className="p-3 text-left">Action</th>
            <th className="p-3 text-left">Case</th>
            <th className="p-3 text-left">Notes</th>
          </tr>
        </thead>
        <tbody>
          {entries.map((entry, idx) => (
            <tr key={idx} className="border-t">
              <td className="p-3">{entry.timestamp}</td>
              <td className="p-3">{entry.user}</td>
              <td className="p-3">{entry.action}</td>
              <td className="p-3">{entry.caseID}</td>
              <td className="p-3">{entry.notes}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}
```

## 🪞 Deployment Options

### Platform Comparison

| Platform | How to Deploy |
|----------|---------------|
| **Notion** | Paste sections as toggle blocks, link buttons to sub-pages |
| **Framer/Webflow** | Import HTML structure, connect button animations |
| **React (Vite)** | Copy components to `/pages`, run `npm run dev` |
| **Vercel** | Connect GitHub repo, auto-deploy on push |
| **Netlify** | Drag & drop build folder or connect repo |

### Vercel Deployment

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel
```

## 🔒 Security & Ethics

### Educational Disclaimers
- ✅ All case data is fictional placeholder content
- ✅ No real client information or legal matters
- ✅ Designed for classroom demonstration only
- ✅ Not intended for actual legal practice

### Best Practices Demonstrated
- Human attorney must review all AI outputs
- Audit trails maintain accountability
- Risk scoring helps identify potential issues
- Version control tracks all changes
- Settings enforce compliance requirements

## 📚 Technology Stack

- **Frontend**: React 18+ with Vite
- **Styling**: Tailwind CSS 3+
- **State Management**: React hooks
- **Routing**: React Router (optional)
- **Build Tool**: Vite
- **Package Manager**: npm/yarn

## 🤝 Contributing

This is an educational prototype. Contributions for educational enhancements are welcome:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/enhancement`)
3. Commit changes (`git commit -am 'Add educational feature'`)
4. Push to branch (`git push origin feature/enhancement`)
5. Open a Pull Request

## 📖 Educational Context

This prototype demonstrates:
- Ethical AI implementation in legal tech
- Human oversight in automated systems
- Transparency and accountability mechanisms
- ADHD-friendly interface design principles
- Compliance-first development approach

## 📝 License

MIT License - See [LICENSE](LICENSE) file for details.

**Educational Use Statement**: This software is provided as-is for educational and demonstration purposes in law school and legal technology courses. It is not intended for use in actual legal practice or client representation.

## 🔗 Related Resources

- [ABA Model Rules on Technology](https://www.americanbar.org/groups/professional_responsibility/publications/model_rules_of_professional_conduct/)
- [Legal Tech Ethics Guidelines](https://www.americanbar.org/groups/law_practice/resources/)
- [Accessibility Compliance Resources](https://www.ada.gov/)

## 📧 Contact

For educational inquiries or collaboration:
- GitHub: [@aaj2127](https://github.com/aaj2127)
- Repository: [justice-seek-ai-accountability-console](https://github.com/aaj2127/justice-seek-ai-accountability-console)

---

**Built with ⚖️ for ethical AI legal education**

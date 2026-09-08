import React, { useState } from 'react';

export default function ReadmeGenerator() {
  const [formData, setFormData] = useState({
    name: 'Fotis Stamatakis',
    role: 'Electrical & Computer Engineering Student | Embedded Hardware Engineer',
    about: 'Focusing on high-speed digital PCB layout, biopotential AFEs, and STM32/ESP32 firmware.',
    githubUser: 'fotis-stamatakis',
    linkedin: 'fotis-stamatakis',
    eeg3DUrl: 'https://raw.githubusercontent.com/.../eeg_3d.png',
    eegLayoutUrl: 'https://raw.githubusercontent.com/.../eeg_layout.png',
  });

  // Pure function to generate the final Markdown
  const generateMarkdown = () => {
    return `# Hi, I'm ${formData.name} 👋
**${formData.role}**

---

### 👨‍💻 About Me
- 🎓 ${formData.about}

---

### 🔬 Featured Hardware Designs

<div align="center">

#### 32-Channel Mixed-Signal EEG Platform
| Altium 3D Render | PCB Routing Layer |
| :---: | :---: |
| <img src="${formData.eeg3DUrl}" width="400" alt="32-Channel EEG 3D Render"> | <img src="${formData.eegLayoutUrl}" width="400" alt="PCB Layout"> |

</div>

---

### 📈 GitHub Stats
![GitHub Stats](https://github-readme-stats.vercel.app/api?username=${formData.githubUser}&show_icons=true&theme=tokyonight)

---

### 📫 Connect With Me
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/${formData.linkedin})
`;
  };

  const [copied, setCopied] = useState(false);

  const handleCopy = () => {
    navigator.clipboard.writeText(generateMarkdown());
    setCopied(true);
    setTimeout(() => setCopied(false), 2000);
  };

  return (
    <div style={{ display: 'flex', gap: '20px', padding: '20px', fontFamily: 'sans-serif' }}>
      {/* Input Section */}
      <div style={{ flex: 1 }}>
        <h2>Configure Profile</h2>
        
        <label>Full Name:</label><br />
        <input 
          type="text" 
          value={formData.name} 
          onChange={(e) => setFormData({...formData, name: e.target.value})} 
          style={{ width: '100%', marginBottom: '10px' }}
        />

        <label>Professional Role:</label><br />
        <input 
          type="text" 
          value={formData.role} 
          onChange={(e) => setFormData({...formData, role: e.target.value})} 
          style={{ width: '100%', marginBottom: '10px' }}
        />

        <label>GitHub Username:</label><br />
        <input 
          type="text" 
          value={formData.githubUser} 
          onChange={(e) => setFormData({...formData, githubUser: e.target.value})} 
          style={{ width: '100%', marginBottom: '10px' }}
        />

        <label>EEG 3D Render Image URL:</label><br />
        <input 
          type="text" 
          value={formData.eeg3DUrl} 
          onChange={(e) => setFormData({...formData, eeg3DUrl: e.target.value})} 
          style={{ width: '100%', marginBottom: '10px' }}
        />
      </div>

      {/* Output / Code Section */}
      <div style={{ flex: 1, backgroundColor: '#f4f4f4', padding: '15px', borderRadius: '8px' }}>
        <div style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
          <h2>Generated Markdown</h2>
          <button onClick={handleCopy}>
            {copied ? 'Copied!' : 'Copy Markdown'}
          </button>
        </div>
        <pre style={{ whiteSpace: 'pre-wrap', wordBreak: 'break-word', fontSize: '12px' }}>
          {generateMarkdown()}
        </pre>
      </div>
    </div>
  );
}

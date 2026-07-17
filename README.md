# Codeforces Analyzer 📊

An interactive, high-performance client-side web application designed to fetch, filter, and visualize competitive programming metrics using the public Codeforces REST API. This tool is optimized to deliver deep analytical insights into user performance, submission trends, and rating progression with zero server-side dependencies.

---

## 🚀 Key Features

### ⚡ Optimized Async Pipeline
* **Concurrent Requests:** Mitigates network and dashboard loading latency by orchestrating parallel asynchronous API requests via `Promise.all`. User profiles and submission histories are fetched simultaneously, bypassing sequential waterfall network bottlenecks.

### 🛡️ High-Integrity Data Filtering
* **Unique Submission Tracking:** Leverages JavaScript `Set` structures to isolate unique, accepted ("OK") submissions. This prevents statistical inflation caused by multiple attempts on the same problem, guaranteeing an accurate representation of solved problem tags and frequencies.

### 📈 Rich Data Visualizations
  * **Dynamic Rendering:** Transforms raw JSON API payloads into responsive, visual charts utilizing Chart.js:
  * **Difficulty Distribution Heatmap:** Clear visualization of solved problems across various rating tiers.
  * **Rating Trajectory Graph:** An interactive chronological timeline tracking contest performance and rating history.

---

## ⚡ Technical Implementations

### 1. Latency Mitigation (Concurrent Fetches)
To keep dashboard load times as close to instant as possible, the application initiates parallel fetches instead of waiting for sequential responses:

```javascript
const [userInfo, userSubmissions] = await Promise.all([
  fetch(`https://codeforces.com/api/user.info?handles=${handle}`),
  fetch(`https://codeforces.com/api/user.status?handle=${handle}`)
]);
```

### 2. Data Integrity Logic (Unique "OK" Submissions)
To filter out redundant submissions and clean the dataset before passing it to the visualization engine:

```javascript
const uniqueSubmissions = new Set();
const filteredData = submissions.filter(sub => {
  if (sub.verdict === "OK" && !uniqueSubmissions.has(sub.problem.name)) {
    uniqueSubmissions.add(sub.problem.name);
    return true;
  }
  return false;
});
```

---

## 🛠️ Tech Stack & Setup

* **Technologies:** HTML5, CSS3, ES6+ JavaScript, Codeforces REST API, Chart.js.
* **Quick Start:** Clone the repository and open the `Analyzer.html` file directly in any modern web browser to run the application locally.

# תוכנית הפעלה: Unity MCP עם Kiro

*בנוי וכתוב על ידי: יובל כהן*

## 📋 סטטוס נוכחי

### ✅ מה שכבר קיים:
- Unity Editor עם החבילה unity-mcp-ollama מותקנת
- Python 3.12.7 מותקן
- Conda מותקן
- Ollama 0.6.5 מותקן
- מודלים זמינים: deepseek-coder:latest, qwen2.5-coder:1.5b, llama3, codellama

### ⚙️ מה שהותקן זה עתה:
- סביבת conda בשם `unity-mcp` נוצרה
- חבילות Python: httpx, mcp, fastapi, uvicorn

---

## 🎯 תוכנית הפעולה (5 שלבים)

### שלב 1: עדכון הגדרות Ollama ✅ (בוצע חלקית)
**מטרה:** להגדיר את המודל deepseek-coder במקום gemma3

**פעולות:**
1. ✅ סביבת conda נוצרה
2. ✅ חבילות Python הותקנו
3. ⏳ עדכון קובץ `local_config.json` - להחליף `gemma3:12b` ל-`deepseek-coder:latest`
4. ⏳ עדכון רשימת המודלים ב-Unity Editor

---

### שלב 2: התקנת החבילה Python ⏳
**מטרה:** להתקין את חבילת unity-mcp בסביבה

**פעולות:**
1. להריץ `pip install -e .` בתיקיית Python
2. לוודא שכל התלויות מותקנות

**זמן משוער:** 2-3 דקות

---

### שלב 3: הפעלת Unity Bridge ⏳
**מטרה:** להפעיל את השרת ב-Unity Editor

**פעולות (ידניות - אתה צריך לעשות):**
1. פתח את Unity Editor
2. לחץ על `Window > Unity MCP`
3. לחץ על `Start Bridge`
4. וודא שהסטטוס הוא "Running"

**זמן משוער:** 1 דקה

---


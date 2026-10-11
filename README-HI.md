# Result Perfect — सुरक्षित एडमिन लॉगिन

यह **तैयार प्रोजेक्ट कोड** है, अभी लाइव/होस्ट की गई वेबसाइट नहीं। इसे चलाने के लिए Node.js होस्टिंग और PostgreSQL डेटाबेस सेटअप करना होगा।

## इसमें क्या सुरक्षित किया गया है?
- सर्वर-साइड एडमिन सत्यापन: सिर्फ `.env` में निर्धारित एक एडमिन अकाउंट
- पासवर्ड/यूज़रनेम ब्राउज़र कोड में नहीं रखे जाते
- PostgreSQL में पोस्ट और सर्वर-साइड लॉगिन सेशन
- HttpOnly, SameSite session cookie; production में Secure cookie
- लॉगिन rate limit, session ID regeneration, CSRF token checks, Helmet security headers
- सिर्फ लॉगिन किए हुए एडमिन को पोस्ट जोड़ने, बदलने और हटाने की अनुमति
- पोस्ट लिंक के लिए HTTPS validation

## चलाने के लिए
1. Node.js 20+ और PostgreSQL की जरूरत है।
2. इस ZIP को extract करें।
3. `.env.example` की कॉपी `.env` नाम से बनाएँ।
4. `.env` में `DATABASE_URL`, `ADMIN_USERNAME`, `ADMIN_PASSWORD`, `SESSION_SECRET` भरें। पासवर्ड कम-से-कम 14 अक्षर का और `SESSION_SECRET` कम-से-कम 32 अक्षर का रखें।
5. `npm install`
6. `npm start`
7. ब्राउज़र में `http://localhost:3000` खोलें।

## ऑनलाइन प्रकाशित करना
- ऐसे Node.js host का उपयोग करें जो persistent managed PostgreSQL database और environment variables देता हो।
- Host के Environment Variables/Secrets में `.env` के मान जोड़ें; `.env` फाइल कभी public repository में upload न करें।
- `NODE_ENV=production`, `DATABASE_SSL=true` और HTTPS enable करें।
- Deploy करने के बाद homepage में नीचे Admin Panel → एडमिन लॉगिन से प्रवेश करें।
- पहली बार सेट किया गया एडमिन यूज़रनेम/पासवर्ड सुरक्षित रखें। `ADMIN_PASSWORD` बदलने के बाद app restart करें।

## जरूरी सीमाएँ
- मैं यहाँ से hosting account नहीं बना सकता, database provider में आपके लिए संसाधन नहीं बना सकता, या इसे आपके नाम से live deploy नहीं कर सकता। Hosting credentials या password चैट में न भेजें।
- अभी initial admin account environment variables से नियंत्रित है; इस प्रोजेक्ट में public registration या password reset route नहीं है।
- पुराने static HTML से इसमें सीधे auto-migration नहीं है। पुराने hard-coded links starter homepage में शामिल किए गए हैं; नए पोस्ट PostgreSQL से लोड होते हैं।
- आधिकारिक लिंक प्रकाशित करने से पहले उन्हें खुद verify करें।

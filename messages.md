# BrightSmile Dental Clinic — Bot Message Scripts

All messages below are written in both English (EN) and Arabic (AR). The bot detects
language at State 0 (checks whether the incoming message contains Arabic script) and
replies in whichever language the user is currently using. If the user switches
language mid-conversation, the bot re-checks the script of each new incoming message
and switches its reply language from that point onward.

---

## State 1 — Greeting + Intent

**EN:**
```
Welcome to BrightSmile Dental Clinic! 😊
Would you like to book an appointment, or do you have a question?

1. Book an appointment
2. Ask a question
```

**AR:**
```
مرحبًا بكم في عيادة برايت سمايل لطب الأسنان! 😊
هل ترغب في حجز موعد، أم لديك سؤال؟

1. حجز موعد
2. طرح سؤال
```

---

## FAQ Loop (triggered when user picks "Ask a question")
A simple lookup — e.g. clinic hours, location, accepted insurance, prices for
common services. After answering, the bot loops back to the State 1 question
("Would you like to book, or do you have another question?").

Sample FAQ entry:

**EN:** "We're open Sat–Thu, 10am–8pm. We're located at [Clinic Address]. Would you like to book an appointment, or ask something else?"

**AR:** "نعمل من السبت إلى الخميس، من الساعة 10 صباحًا حتى 8 مساءً. عنواننا [عنوان العيادة]. هل ترغب في حجز موعد أم لديك سؤال آخر؟"

---

## State 2 — Service

**EN:**
```
Great! Which service are you interested in?

1. Cleaning & Checkup
2. Teeth Whitening
3. Braces Consultation
4. Filling / Extraction
5. Root Canal
```

**AR:**
```
رائع! ما هي الخدمة التي تهمك؟

1. تنظيف وفحص
2. تبييض الأسنان
3. استشارة تقويم الأسنان
4. حشو / خلع
5. علاج عصب
```

---

## State 3 — Timing

**EN:**
```
Perfect. When would you like your appointment?
(e.g. "tomorrow morning", "this Friday", or a specific date)
```

**AR:**
```
ممتاز. متى ترغب في تحديد موعدك؟
(مثال: "غدًا صباحًا"، "يوم الجمعة القادم"، أو تاريخ محدد)
```

---

## State 4 — Offer Slots

**EN:**
```
Here are our available slots for [requested day]:

1. 10:00 AM
2. 2:30 PM
3. 5:00 PM

Please reply with the number of your preferred slot.
```

**AR:**
```
إليك المواعيد المتاحة ليوم [اليوم المطلوب]:

1. 10:00 صباحًا
2. 2:30 ظهرًا
3. 5:00 مساءً

يرجى الرد برقم الموعد الذي يناسبك.
```

---

## State 5 — Confirm

**EN:**
```
You're all set! ✅
Service: [Service Name]
Date: [Date]
Time: [Time]

We look forward to seeing you at BrightSmile Dental Clinic. Reply "cancel" anytime if you need to change this.
```

**AR:**
```
تم تأكيد حجزك! ✅
الخدمة: [اسم الخدمة]
التاريخ: [التاريخ]
الوقت: [الوقت]

نتطلع لرؤيتك في عيادة برايت سمايل لطب الأسنان. يمكنك الرد بكلمة "إلغاء" في أي وقت إذا أردت تغيير الموعد.
```

---

## Nudge 1 — +1 hour of silence
*(Free-form message — still within the 24h customer service window, no template needed)*

**EN:**
```
Hi! Just checking in — are you still there? Happy to help you finish booking your appointment whenever you're ready. 😊
```

**AR:**
```
مرحبًا! أردت فقط الاطمئنان — هل ما زلت معنا؟ يسعدنا مساعدتك في إتمام حجز موعدك متى ما كنت جاهزًا. 😊
```

---

## Nudge 2 — +24 hours of silence
**⚠️ Requires a pre-approved WhatsApp Template message (outside the 24h free-form window). Not sending a real template in this phase — this is the intended content to submit for Meta approval later.**

**EN (template concept):**
```
Hi {{1}}, we noticed you started booking an appointment with BrightSmile Dental Clinic but didn't finish. We've saved your spot — reply here to continue anytime.
```

**AR (template concept):**
```
مرحبًا {{1}}، لاحظنا أنك بدأت بحجز موعد في عيادة برايت سمايل لطب الأسنان ولم تكمل العملية. لقد احتفظنا بمكانك — يمكنك الرد هنا لإكمال الحجز في أي وقت.
```

---

## Nudge 3 — +72 hours of silence
**⚠️ Requires a pre-approved WhatsApp Template message.**

**EN (template concept):**
```
Hi {{1}}, this is a final reminder from BrightSmile Dental Clinic — your appointment slot is still open. Reply here if you'd like to book, or we'll release the slot.
```

**AR (template concept):**
```
مرحبًا {{1}}، هذه رسالة تذكير أخيرة من عيادة برايت سمايل لطب الأسنان — لا يزال موعدك متاحًا. يرجى الرد هنا إذا رغبت بالحجز، وإلا سيتم إلغاء حجز الموعد.
```

*(If no response after this, the lead is marked as "lost" internally — no further messages are sent.)*

---

## Human Handoff Message
*(Triggered for: medical/health questions, complaints, price negotiation, or any off-script message)*

**EN:**
```
This is something one of our team members can help you with best. I'm connecting you with a BrightSmile staff member now — they'll be with you shortly! 🙏
```

**AR:**
```
هذا الأمر يمكن لأحد أفراد فريقنا مساعدتك فيه بشكل أفضل. سأقوم بتحويلك الآن إلى أحد موظفي برايت سمايل — سيتواصل معك قريبًا! 🙏
```

---

## Reusable Config Object (Bonus)

```json
{
  "clinic_name": "BrightSmile Dental Clinic",
  "services": [
    "Cleaning & Checkup",
    "Teeth Whitening",
    "Braces Consultation",
    "Filling / Extraction",
    "Root Canal"
  ],
  "calendar_id": "mock_calendar_v1",
  "handoff_contact": "+92XXXXXXXXX",
  "reminder_lead_time_hours": 24,
  "languages": ["en", "ar"],
  "faq": [
    {
      "question_keywords": ["hours", "open", "ساعات", "دوام"],
      "answer_en": "We're open Sat-Thu, 10am-8pm.",
      "answer_ar": "نعمل من السبت إلى الخميس، من 10 صباحًا حتى 8 مساءً."
    },
    {
      "question_keywords": ["location", "address", "عنوان", "موقع"],
      "answer_en": "We're located at [Clinic Address].",
      "answer_ar": "عنواننا [عنوان العيادة]."
    }
  ]
}
```

## Why the Human Handoff Step Matters
The bot should never improvise on medical/health questions, complaints, or price
negotiation because these carry real risk: a wrong medical answer could harm a
patient's health or the clinic's liability, an unhandled complaint can lose a
customer permanently, and improvised pricing discounts undercut the business.
Handing off to a human keeps the bot inside its safe, scripted lane and routes
anything sensitive to someone who can actually take responsibility for the answer.

# MVP Shipping Guide: Ship Fast, Iterate Later 🚀

The pragmatic guide to shipping MVPs using AI tools, vibe coding, and smart debt management.

---

## 🎯 The MVP Philosophy

**Core Principle:** Working software in users' hands > Perfect code in your repo

```
Perfect code that never ships = $0 value
Messy code that ships today = $∞ potential value
```

**The Trap:**
```
❌ Vibe → Refine → Polish → Perfect → Never ship
✅ Vibe → Ship → Learn → Iterate → Ship again
```

---

## 🚀 The MVP Shipping Timeline

### Week 1: Vibe & Ship (80% time)

**Goal:** Get something working in front of users ASAP

**Allowed Shortcuts:**
- ✅ `any` types everywhere
- ✅ Hardcoded values
- ✅ Copy-pasted code
- ✅ No tests (gasp!)
- ✅ Inline everything
- ✅ Console.log debugging
- ✅ TODO comments everywhere
- ✅ Skip documentation

**Tools:** Cursor Composer + Cursor Chat + Copilot (vibe mode)

**Daily Workflow:**
```bash
# Morning: Vibe coding (no interruptions)
9am-12pm: Pure creation mode, AI-assisted

# Afternoon: Ship it
1pm-2pm: Quick manual test
2pm-3pm: Deploy to staging/production
3pm-4pm: Monitor, fix critical bugs only

# End of day
git add .
git commit -m "vibe: [feature] - shipped 🚀"
```

**Success Criteria:**
- [ ] Feature works in happy path
- [ ] No critical crashes
- [ ] Deployed and accessible
- [ ] 1+ user can use it

**Explicitly DON'T do:**
- ❌ Refactor anything
- ❌ Write tests
- ❌ Perfect the UI
- ❌ Handle all edge cases
- ❌ Optimize performance
- ❌ Document code

---

### Week 2: Learn & Iterate (20% cleanup, 80% new features)

**Goal:** Learn from real usage, add most-requested features

**Minimal Cleanup:**
- Fix bugs that block users
- Add basic error handling for crashes
- Create ONE safety point: `BEFORE_ITERATION_2`

**Keep Shipping:**
- More features based on user feedback
- Quick fixes, quick deploys
- Maintain velocity

**Friday Afternoon (2 hours):**
```bash
# Create safety point
git tag -a MVP_WEEK2_STABLE -m "Stable after week 2"

# Quick cleanup (pick ONE)
- Extract most duplicated code OR
- Fix worst type safety issues OR  
- Add error boundaries OR
- Clean up config files

# Commit and done
git commit -m "cleanup: minimal debt payment"
```

---

### Month 1: Stabilize (50/50 features vs. cleanup)

**Goal:** Make it stable enough to grow, but keep shipping

**Now You Can:**
- Add tests for critical paths
- Refactor worst code smells
- Document public APIs
- Set up proper CI/CD

**But Still:**
- Ship features weekly
- Learn from users
- Stay scrappy

---

## 🎨 The MVP Stack Decision

**Choose stack by shipping speed, not by "correctness":**

| Goal | Fastest Stack | Ship Time | Why |
|------|---------------|-----------|-----|
| Landing page | HTML + Tailwind + Netlify | 2 hours | No build step, instant deploy |
| Web app | Next.js + Vercel | 1 day | File routing, deploy on push |
| Mobile app | React Native + Expo | 2 days | Hot reload, TestFlight easy |
| API | FastAPI + Railway | 4 hours | Auto docs, one-click deploy |
| Dashboard | React + Supabase | 1 day | Backend included, auth built-in |
| Chrome extension | Vite + manifest.json | 4 hours | Fast builds, quick publish |

**The Rule:** Pick the stack that gets you to first user fastest, not the one you'll use at scale.

---

## 🛠️ MVP Tool Selection

### Phase 1: Vibe & Ship (Week 1)

**Primary Tools:**
- **Cursor Composer** - Scaffold entire features
- **Cursor Chat** - Quick iterations  
- **Copilot** - Boilerplate generation

**Avoid:**
- ❌ Gemini (too much refinement)
- ❌ Cline (too much testing)
- ❌ Manual coding (too slow)

### Phase 2: Learn & Iterate (Week 2-4)

**Add:**
- **Cline** - Run tests, deploy
- **Gemini** - Fix only critical issues

**Keep using:**
- Cursor for new features

### Phase 3: Stabilize (Month 2+)

**Full toolkit:**
- Cursor Composer - Architecture
- Cursor Chat - Iterations
- Cline - Testing & deployment
- Gemini - Code quality
- Copilot - Always on

---

## ⚡ The MVP Vibe Coding Playbook

### 1. Scaffold with Composer (30 min)

**Prompt:**
```
Create a [feature] for my [stack] project that:
- Works end-to-end (frontend + backend + data)
- Uses dummy data where needed
- Has basic error handling (just show error messages)
- Gets me to "working" fastest

Don't worry about:
- Perfect architecture
- Type safety
- Performance optimization
- Edge cases

Just make it WORK so I can show users.
```

**Example (Next.js SaaS):**
```
Create a user dashboard that:
- Shows user profile info
- Lists their recent activities
- Has a simple form to update settings
- Connects to Supabase

Use any types, hardcode where helpful, just get it working.
I'll refine later.
```

### 2. Iterate with Chat (2-3 hours)

**Rapid-fire prompts:**
```
"Add a loading spinner"
"Make the button bigger"
"Change color to blue"
"Add error message if form fails"
"Make it work on mobile"
```

**No thinking, just shipping.**

### 3. Deploy with Cline (15 min)

```bash
# Ask Cline
"Deploy this to Vercel/Netlify/Railway"

# Or manually
git push origin main  # If auto-deploy configured
```

### 4. Test in Production (30 min)

**Manual testing checklist (3 minutes):**
- [ ] Page loads
- [ ] Main button works
- [ ] Form submits
- [ ] Data displays
- [ ] Mobile doesn't explode

**Ship it.** 🚀

---

## 🎯 MVP Success Metrics

**Week 1:**
- ✅ Deployed? (Yes/No)
- ✅ 1+ user tried it? (Yes/No)
- ✅ Major feature works? (Yes/No)

**That's it.** Everything else is noise.

**Week 2-4:**
- ✅ Daily active users (any number > 0)
- ✅ Core user flow completion rate (> 50%)
- ✅ Critical bugs (< 5)

**NOT measured:**
- ❌ Code quality
- ❌ Test coverage
- ❌ Type safety
- ❌ Performance benchmarks
- ❌ Tech debt

**Those come later.**

---

## 🚫 The "Do NOT Do" List for MVPs

### Don't Refine Before Shipping

```
❌ "Let me clean this up before deploying"
✅ "Ship now, clean later"

❌ "The types are messy, let me fix"
✅ "Types work, ship it"

❌ "I should add tests first"
✅ "Tests after first user"

❌ "Let me write documentation"
✅ "Code is documentation for MVP"
```

### Don't Optimize Prematurely

```
❌ "This could be faster with caching"
✅ "It loads in 2 seconds, good enough"

❌ "Let me use Redis for performance"
✅ "In-memory is fine for MVP"

❌ "Database query needs indexing"
✅ "Query takes 100ms, who cares"
```

### Don't Handle Every Edge Case

```
❌ "What if user enters emoji in name?"
✅ "I'll fix if it actually happens"

❌ "What if they have 10,000 items?"
✅ "They have 0 items, not a problem yet"

❌ "What if server goes down?"
✅ "I'll restart it if it crashes"
```

### Don't Build for Scale

```
❌ "Let me set up Kubernetes"
✅ "Vercel/Netlify/Railway is fine"

❌ "Need microservices architecture"
✅ "Monolith ships faster"

❌ "Should design for 1M users"
✅ "Let me get to 10 users first"
```

---

## 💰 MVP Debt Management

**The Debt Hierarchy:**

```
🔴 CRITICAL DEBT (Fix immediately)
   - Security vulnerabilities
   - Data loss bugs
   - User-blocking crashes

🟠 HIGH DEBT (Fix within 2 weeks)
   - Frequent bugs
   - Painful workflow for users
   - Scaling bottlenecks (when they appear)

🟡 MEDIUM DEBT (Fix when convenient)
   - Code duplication
   - Missing tests
   - Type safety
   - Performance "could be better"

🟢 LOW DEBT (Maybe never fix)
   - Code comments
   - Perfect architecture
   - 100% test coverage
   - Documentation
```

**Debt Payment Schedule:**

```
Week 1: Pay ZERO debt (just ship)
Week 2: Pay critical debt only
Week 3-4: Pay critical + high debt
Month 2: Start medium debt if time allows
Month 3+: Low debt if bored
```

---

## 🎪 Real MVP Examples

### Example 1: SaaS Dashboard (Next.js)

**Week 1 (Vibe & Ship):**
```typescript
// pages/dashboard.tsx
export default function Dashboard() {
  const [data, setData] = useState<any>(null); // any = fine!
  
  useEffect(() => {
    fetch('/api/data').then(r => r.json()).then(setData);
  }, []);
  
  return (
    <div className="p-8">
      <h1>Dashboard</h1>
      {data?.map((item: any) => (
        <div key={item.id}>{item.name}</div>
      ))}
    </div>
  );
}

// Shipped in 4 hours ✅
```

**Week 4 (After user feedback):**
```typescript
// Still mostly the same, just fixed crashes
export default function Dashboard() {
  const { data, loading, error } = useDashboardData();
  
  if (loading) return <Spinner />;
  if (error) return <Error message={error.message} />;
  
  return (
    <div className="p-8">
      <h1>Dashboard</h1>
      {data.map(item => (
        <DashboardCard key={item.id} item={item} />
      ))}
    </div>
  );
}

// Better, but still shipping fast ✅
```

### Example 2: Chrome Extension (Vite)

**Week 1:**
```javascript
// content.js - Hardcoded everything
chrome.runtime.onMessage.addListener((msg) => {
  if (msg.action === 'highlight') {
    document.body.style.backgroundColor = 'yellow'; // Lol
  }
});

// Shipped to Chrome Web Store in 6 hours ✅
```

**Week 3 (After 50 users):**
```javascript
// content.js - Added user preferences
chrome.storage.sync.get(['color'], (result) => {
  if (msg.action === 'highlight') {
    document.body.style.backgroundColor = result.color || 'yellow';
  }
});

// Better, still simple ✅
```

### Example 3: API (FastAPI)

**Week 1:**
```python
# main.py
@app.post("/users")
def create_user(name: str, email: str):
    # No validation, no database, just works
    users.append({"id": len(users), "name": name, "email": email})
    return {"success": True}

# Deployed to Railway in 2 hours ✅
```

**Week 2 (After first paying customer):**
```python
from pydantic import BaseModel, EmailStr

class UserCreate(BaseModel):
    name: str
    email: EmailStr

@app.post("/users")
def create_user(user: UserCreate):
    # Added validation, still in-memory
    users.append(user.dict())
    return {"success": True}

# Better, still shipping ✅
```

---

## 🔄 The Iteration Loop

```
Ship → Learn → Decide → Ship again

Week 1: Ship MVP
   ↓
Week 2: Learn from users
   ↓
Week 3: Decide what to fix/add
   ↓
Week 4: Ship improvements
   ↓
Repeat forever
```

**After Each Iteration:**

```bash
# Create safety point
git tag -a ITERATION_$N -m "End of iteration $N"

# Quick retrospective (5 min)
echo "## Iteration $N" >> ITERATIONS.md
echo "Shipped: [features]" >> ITERATIONS.md
echo "Learned: [insights]" >> ITERATIONS.md
echo "Next: [priorities]" >> ITERATIONS.md

# Keep moving
```

---

## 🎓 MVP Anti-Patterns to Avoid

### 1. The Perfectionist Trap

```
❌ "I'll ship when it's perfect"
✅ "I'll perfect it when it ships"
```

**Reality:** Perfect is the enemy of done.

### 2. The Premature Scaling Trap

```
❌ "Need to handle 1M users from day 1"
✅ "Let me get 100 users first"
```

**Reality:** 99% of MVPs never hit scale problems.

### 3. The Feature Creep Trap

```
❌ "Just one more feature before launch..."
✅ "Launch now, add features based on feedback"
```

**Reality:** Users want ONE thing that works, not ten broken things.

### 4. The Tech Debt Anxiety Trap

```
❌ "Can't ship with this much debt"
✅ "Ship now, pay debt from revenue"
```

**Reality:** Debt only matters if you survive to pay it.

### 5. The Refactor Trap

```
❌ "Let me refactor before adding features"
✅ "Add features, refactor only what breaks"
```

**Reality:** Refactoring without user pressure is procrastination.

---

## 📊 MVP vs. Production Comparison

| Aspect | MVP (Week 1) | Production (Month 6+) |
|--------|--------------|----------------------|
| Type safety | any everywhere | Proper types |
| Tests | None | Critical paths |
| Error handling | Basic | Comprehensive |
| Performance | Good enough | Optimized |
| Documentation | None | API docs |
| Architecture | Spaghetti | Clean |
| Deployment | Manual push | CI/CD |
| Monitoring | Console logs | Full observability |
| Security | Basic auth | Hardened |
| Scalability | Single server | Load balanced |

**The Journey:** Left → Right over time, based on actual need.

---

## 🛡️ The One Safety Rule for MVPs

**Create ONE safety point before first deploy:**

```bash
git tag -a MVP_LAUNCH -m "First launch - safety point"
git push origin MVP_LAUNCH
```

**Why:**
- If everything breaks, rollback to this
- If pivot needed, start from here
- If investors ask "show me v1", this is it

**That's it.** One tag, infinite peace of mind.

---

## 🎯 MVP Shipping Checklist

### Before First Deploy

- [ ] Core feature works (happy path)
- [ ] No immediate crashes on load
- [ ] Can be accessed by others
- [ ] Safety point created
- [ ] Deploy command documented

### After First Deploy

- [ ] Shared with 1+ user
- [ ] Monitoring logs (even just console)
- [ ] Way to rollback (safety point)
- [ ] Next feature prioritized

### NOT Required

- [ ] ~~Tests~~
- [ ] ~~Perfect types~~
- [ ] ~~Documentation~~
- [ ] ~~Refactored code~~
- [ ] ~~Performance optimization~~
- [ ] ~~Edge case handling~~
- [ ] ~~Scalability planning~~

---

## 💡 The MVP Mindset

**Remember:**

1. **Ship beats perfect**
   - Shipped code > perfect code
   - User feedback > your assumptions
   - Revenue > tech debt anxiety

2. **Iterate beats planning**
   - Build → Measure → Learn
   - Feedback loops > master plans
   - Adaptation > prediction

3. **Speed beats scale**
   - Fast to market > built to scale
   - Quick pivots > rigid architecture
   - User validation > engineering beauty

4. **Done beats perfect**
   - 80% solution shipped today > 100% solution never
   - Working features > perfect code
   - Users in hand > plans in head

---

## 🚀 The Ultimate MVP Command

```bash
# The only command that matters
git add .
git commit -m "vibe: MVP - ship it 🚀"
git push origin main

# Everything else is details
```

---

## 🎊 Success Stories

**Real MVPs that shipped fast:**

- **Airbnb:** 3 air mattresses, static site, no booking system
- **Dropbox:** Video demo before product existed
- **Stripe:** Just 7 API calls, no dashboard
- **Instagram:** Photo filters only, no stories/reels/etc
- **Twitter:** SMS-based microblogging, no features

**They all shipped fast, iterated later, and won.**

---

## 📝 Your MVP Plan

**Fill this out NOW:**

```markdown
## My MVP

**What:** [One sentence]

**For whom:** [Target user]

**Core feature:** [The ONE thing that works]

**Ship date:** [This week]

**Success metric:** [1+ user used it]

**Tech stack:** [Whatever's fastest]

**Time budget:** [40 hours max]
```

**Then stop planning and start vibing.** 🎵

---

**The Mantra:**

> "Ship fast, iterate later. Perfect is the enemy of done. Revenue beats refactoring. Users beat opinions. Done beats perfect."

**Now go ship something.** 🚀

---

**Last Updated:** 2025-11-18  
**Status:** ✅ Ready to Ship  
**Next Action:** Close this doc, start vibing

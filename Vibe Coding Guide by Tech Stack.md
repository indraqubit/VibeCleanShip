# Vibe Coding Guide by Tech Stack

How to vibe code effectively across different technology stacks, with stack-specific workflows and cleanup strategies.

---

## General Vibe Coding Principles

**Universal truths across all stacks:**

1. **Vibe = Speed + Exploration** - Prioritize working code over perfect architecture
2. **AI is your pair programmer** - Let it handle boilerplate, you handle creativity
3. **Commit early, commit often** - `vibe:` commits are safe spaces
4. **Cleanup is mandatory** - Not optional, just deferred
5. **Know your stack's dangers** - Each stack has unique footguns

---

## Web Development Stacks

### React + TypeScript + Tailwind

**Ideal for:** UI/UX exploration, rapid prototyping, interactive features

#### Vibe Mode Characteristics

**Speed boosters:**
- ✅ Hot reload = instant feedback
- ✅ Component composition = easy iteration
- ✅ Tailwind = no CSS context switching
- ✅ AI excellent at React patterns

**Common vibe outputs:**
- Nested component trees (hard to follow)
- Inline styles mixed with Tailwind
- Props drilling everywhere
- "any" types scattered around
- Duplicated logic across components
- No error boundaries

#### Vibe Workflow

```typescript
// 1. VIBE: Get it on screen fast
function MyFeature() {
  const [data, setData] = useState<any>(null); // any is OK during vibe
  
  // Inline everything, who cares
  useEffect(() => {
    fetch('/api/data').then(r => r.json()).then(setData);
  }, []);
  
  return (
    <div className="p-4 bg-blue-500 text-white rounded-lg shadow-md">
      {data?.items?.map((item: any) => (
        <div key={item.id} className="mb-2">
          {item.name}
        </div>
      ))}
    </div>
  );
}
```

**AI Prompt for Vibe:**
```
Create a React component with TypeScript that:
- Fetches data from [API]
- Displays [UI element]
- Uses Tailwind for styling
- Make it work quickly, don't worry about optimization
```

#### Post-Vibe Cleanup Priorities

**Stage 1: Type Safety** (Tool: Cursor Chat)
```typescript
// Define proper types
interface DataItem {
  id: string;
  name: string;
  timestamp: Date;
}

interface ApiResponse {
  items: DataItem[];
  total: number;
}

// Replace any types
const [data, setData] = useState<ApiResponse | null>(null);
```

**Stage 2: Extract Components** (Tool: Cursor Composer)
```typescript
// Extract reusable parts
function DataCard({ item }: { item: DataItem }) {
  return (
    <div className="mb-2">
      <h3>{item.name}</h3>
      <time>{item.timestamp}</time>
    </div>
  );
}
```

**Stage 3: Custom Hooks** (Tool: Gemini)
```typescript
// Extract data fetching
function useDataFetch(url: string) {
  const [data, setData] = useState<ApiResponse | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);
  
  useEffect(() => {
    fetch(url)
      .then(r => r.json())
      .then(setData)
      .catch(setError)
      .finally(() => setLoading(false));
  }, [url]);
  
  return { data, loading, error };
}
```

**Cleanup Checklist:**
- [ ] No `any` types
- [ ] Components < 100 lines
- [ ] Custom hooks for shared logic
- [ ] Error boundaries added
- [ ] Loading states handled
- [ ] Accessibility (a11y) attributes
- [ ] Responsive design verified

---

### Next.js + Server Actions

**Ideal for:** Full-stack features, API routes, server-side logic

#### Vibe Mode Characteristics

**Speed boosters:**
- ✅ Server actions = no API boilerplate
- ✅ File-based routing = intuitive structure
- ✅ TypeScript across stack = type safety

**Common vibe outputs:**
- Server/client boundary confusion
- Missing error handling in server actions
- No loading states
- Hardcoded data in components
- Overfetching data

#### Vibe Workflow

```typescript
// app/dashboard/page.tsx
// VIBE: Just make it work
export default async function Dashboard() {
  const data = await fetch('https://api.example.com/data').then(r => r.json());
  
  return (
    <div>
      <h1>Dashboard</h1>
      {data.map((item: any) => (
        <div key={item.id}>{item.title}</div>
      ))}
    </div>
  );
}

// Server action - vibe style
'use server'
export async function updateData(formData: FormData) {
  const db = await getDB();
  await db.update(formData.get('id'), formData.get('value'));
  revalidatePath('/dashboard');
}
```

#### Post-Vibe Cleanup Priorities

**Stage 1: Proper Data Layer** (Tool: Cursor Composer)
```typescript
// lib/data.ts - Centralized data fetching
export async function getDashboardData(): Promise<DashboardData> {
  const response = await fetch('https://api.example.com/data', {
    next: { revalidate: 60 } // Cache strategy
  });
  
  if (!response.ok) {
    throw new Error('Failed to fetch dashboard data');
  }
  
  return response.json();
}
```

**Stage 2: Error Boundaries**
```typescript
// app/dashboard/error.tsx
'use client'
export default function Error({ error, reset }: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button onClick={reset}>Try again</button>
    </div>
  );
}
```

**Stage 3: Loading States**
```typescript
// app/dashboard/loading.tsx
export default function Loading() {
  return <DashboardSkeleton />;
}
```

**Cleanup Checklist:**
- [ ] Server/client components clearly marked
- [ ] Error boundaries on all routes
- [ ] Loading states for async operations
- [ ] Proper caching strategies
- [ ] Zod validation on server actions
- [ ] CSRF protection considered

---

### Node.js + Express + PostgreSQL

**Ideal for:** REST APIs, backend services, data processing

#### Vibe Mode Characteristics

**Speed boosters:**
- ✅ Fast iteration on endpoints
- ✅ Easy to test with Postman/curl
- ✅ SQL = direct data access

**Common vibe outputs:**
- No input validation
- SQL injection vulnerabilities
- Missing error handling
- Hardcoded database queries
- No connection pooling
- Sync operations blocking event loop

#### Vibe Workflow

```typescript
// VIBE: Quick endpoint
app.get('/api/users/:id', async (req, res) => {
  const user = await db.query(
    `SELECT * FROM users WHERE id = ${req.params.id}` // SQL injection!
  );
  res.json(user.rows[0]);
});

app.post('/api/users', async (req, res) => {
  const { name, email } = req.body; // No validation!
  await db.query(
    'INSERT INTO users (name, email) VALUES ($1, $2)',
    [name, email]
  );
  res.json({ success: true });
});
```

**AI Prompt for Vibe:**
```
Create an Express.js endpoint that:
- Accepts [data] via POST
- Stores in PostgreSQL
- Returns [response]
Get it working fast, I'll add validation later
```

#### Post-Vibe Cleanup Priorities

**Stage 1: Security** (Tool: Cline - test for vulnerabilities)
```typescript
// Add input validation with Zod
import { z } from 'zod';

const userSchema = z.object({
  name: z.string().min(2).max(100),
  email: z.string().email(),
});

app.post('/api/users', async (req, res) => {
  try {
    const validated = userSchema.parse(req.body);
    // Now safe to use validated.name, validated.email
  } catch (error) {
    return res.status(400).json({ error: 'Invalid input' });
  }
});
```

**Stage 2: Proper Error Handling** (Tool: Cursor Chat)
```typescript
// Centralized error handler
app.use((err: Error, req: Request, res: Response, next: NextFunction) => {
  console.error(err.stack);
  res.status(500).json({ 
    error: 'Internal server error',
    ...(process.env.NODE_ENV === 'development' && { details: err.message })
  });
});

// Async error wrapper
const asyncHandler = (fn: Function) => (req: Request, res: Response, next: NextFunction) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};
```

**Stage 3: Database Layer** (Tool: Cursor Composer)
```typescript
// Separate data access layer
class UserRepository {
  async findById(id: string): Promise<User | null> {
    const result = await pool.query(
      'SELECT * FROM users WHERE id = $1',
      [id]
    );
    return result.rows[0] || null;
  }
  
  async create(data: CreateUserData): Promise<User> {
    const result = await pool.query(
      'INSERT INTO users (name, email) VALUES ($1, $2) RETURNING *',
      [data.name, data.email]
    );
    return result.rows[0];
  }
}
```

**Cleanup Checklist:**
- [ ] All inputs validated (Zod/Joi)
- [ ] Parameterized queries (no SQL injection)
- [ ] Proper error handling middleware
- [ ] Connection pooling configured
- [ ] Rate limiting on public endpoints
- [ ] Logging (Winston/Pino)
- [ ] Health check endpoint
- [ ] Environment variables validated

---

## Native/Systems Programming

### C++17/JUCE 8 (Audio)

**Ideal for:** DSP algorithms, audio effects, plugin features

#### Vibe Mode Characteristics

**Speed boosters:**
- ✅ AI good at algorithm translation
- ✅ JUCE examples abundant
- ✅ Fast compile times (with good setup)

**Common vibe outputs:**
- Memory leaks
- Non-real-time-safe audio code
- Missing const correctness
- Raw pointers everywhere
- Allocation in audio thread
- No RAII

#### Vibe Workflow

```cpp
// VIBE: Get the algorithm working
class SimpleReverb : public juce::AudioProcessor
{
public:
    void processBlock(juce::AudioBuffer<float>& buffer) override
    {
        // Quick and dirty reverb
        float* delayBuffer = new float[48000]; // LEAK! ALLOCATION!
        
        for (int channel = 0; channel < buffer.getNumChannels(); ++channel)
        {
            float* data = buffer.getWritePointer(channel);
            
            for (int i = 0; i < buffer.getNumSamples(); ++i)
            {
                delayBuffer[i % 48000] = data[i];
                data[i] += delayBuffer[(i - 12000) % 48000] * 0.5f;
            }
        }
        // Never freed!
    }
};
```

**AI Prompt for Vibe:**
```
Create a JUCE audio processor that implements [algorithm].
Focus on getting the DSP working, I'll optimize later.
Use simple, clear code.
```

#### Post-Vibe Cleanup Priorities

**Stage 1: Memory Safety** (Tool: Cline - run ASAN)
```cpp
class SimpleReverb : public juce::AudioProcessor
{
public:
    SimpleReverb() : delayBuffer(1, 48000) {} // Pre-allocate in constructor
    
    void processBlock(juce::AudioBuffer<float>& buffer) override
    {
        // No allocations in audio thread
        for (int channel = 0; channel < buffer.getNumChannels(); ++channel)
        {
            auto* data = buffer.getWritePointer(channel);
            auto* delay = delayBuffer.getWritePointer(0);
            
            for (int i = 0; i < buffer.getNumSamples(); ++i)
            {
                const int writePos = (delayPos + i) % 48000;
                const int readPos = (delayPos + i - 12000 + 48000) % 48000;
                
                delay[writePos] = data[i];
                data[i] += delay[readPos] * 0.5f;
            }
        }
        delayPos = (delayPos + buffer.getNumSamples()) % 48000;
    }
    
private:
    juce::AudioBuffer<float> delayBuffer;
    int delayPos = 0;
};
```

**Stage 2: Real-Time Safety** (Tool: Gemini)
```cpp
// Use juce::dsp for guaranteed RT-safety
class SimpleReverb : public juce::AudioProcessor
{
    void prepare(const juce::dsp::ProcessSpec& spec) override
    {
        reverb.prepare(spec);
    }
    
    void processBlock(juce::AudioBuffer<float>& buffer) override
    {
        juce::dsp::AudioBlock<float> block(buffer);
        juce::dsp::ProcessContextReplacing<float> context(block);
        reverb.process(context);
    }
    
private:
    juce::dsp::Reverb reverb;
};
```

**Stage 3: Performance** (Tool: Cline - profile)
```cpp
// Optimize with SIMD
void processBlock(juce::AudioBuffer<float>& buffer) override
{
    for (int channel = 0; channel < buffer.getNumChannels(); ++channel)
    {
        // Use JUCE's optimized operations
        juce::FloatVectorOperations::multiply(
            buffer.getWritePointer(channel),
            gainSmoothed.getNextValue(),
            buffer.getNumSamples()
        );
    }
}
```

**Cleanup Checklist:**
- [ ] Zero memory leaks (verified with ASAN)
- [ ] No allocations in processBlock
- [ ] All resources use RAII
- [ ] Smart pointers for ownership
- [ ] Const correctness throughout
- [ ] Thread safety documented
- [ ] Performance profiled
- [ ] Plugin validator passes

---

### Rust + Tokio (Async)

**Ideal for:** Concurrent services, performance-critical code, CLI tools

#### Vibe Mode Characteristics

**Speed boosters:**
- ✅ Compiler catches most bugs
- ✅ Cargo makes dependencies easy
- ✅ AI decent at Rust patterns

**Common vibe outputs:**
- `.unwrap()` everywhere
- `clone()` to satisfy borrow checker
- Async/sync mixing issues
- Missing error context
- Inefficient data structures

#### Vibe Workflow

```rust
// VIBE: Make it compile
async fn fetch_user(id: String) -> User {
    let client = reqwest::Client::new();
    let response = client
        .get(&format!("https://api.example.com/users/{}", id))
        .send()
        .await
        .unwrap(); // Panic on error!
    
    response.json::<User>().await.unwrap()
}

async fn process_users(ids: Vec<String>) -> Vec<User> {
    let mut users = Vec::new();
    for id in ids {
        users.push(fetch_user(id.clone()).await); // Sequential! Clone!
    }
    users
}
```

**AI Prompt for Vibe:**
```
Write async Rust code with Tokio that:
- Fetches data from [API]
- Processes [data]
- Returns [result]
Just make it work, I'll handle errors properly later
```

#### Post-Vibe Cleanup Priorities

**Stage 1: Proper Error Handling** (Tool: Cursor Chat)
```rust
use anyhow::{Context, Result};

async fn fetch_user(id: &str) -> Result<User> {
    let client = reqwest::Client::new();
    let response = client
        .get(&format!("https://api.example.com/users/{}", id))
        .send()
        .await
        .context("Failed to send request")?;
    
    response
        .json::<User>()
        .await
        .context("Failed to parse user JSON")
}
```

**Stage 2: Concurrent Execution** (Tool: Gemini)
```rust
use futures::future;

async fn process_users(ids: &[String]) -> Result<Vec<User>> {
    // Parallel fetching
    let futures: Vec<_> = ids
        .iter()
        .map(|id| fetch_user(id))
        .collect();
    
    future::try_join_all(futures)
        .await
        .context("Failed to fetch all users")
}
```

**Stage 3: Optimize Allocations** (Tool: Gemini)
```rust
// Pre-allocate capacity
async fn process_users(ids: &[String]) -> Result<Vec<User>> {
    let mut users = Vec::with_capacity(ids.len());
    
    // Batch processing
    for chunk in ids.chunks(10) {
        let chunk_users = fetch_chunk(chunk).await?;
        users.extend(chunk_users);
    }
    
    Ok(users)
}
```

**Cleanup Checklist:**
- [ ] No `.unwrap()` (use `?` or proper handling)
- [ ] Errors have context (anyhow/thiserror)
- [ ] Unnecessary clones removed
- [ ] Async operations run concurrently
- [ ] Proper cancellation handling
- [ ] Tests with `tokio::test`
- [ ] Clippy warnings addressed

---

## Mobile Development

### React Native + Expo

**Ideal for:** Mobile app features, cross-platform UI

#### Vibe Mode Characteristics

**Speed boosters:**
- ✅ Expo Go = instant preview
- ✅ Hot reload on device
- ✅ AI good at React patterns

**Common vibe outputs:**
- Platform-specific bugs ignored
- Poor performance on Android
- Memory leaks in navigation
- Unoptimized images
- Missing offline support

#### Vibe Workflow

```typescript
// VIBE: Get it on screen
function UserProfile({ userId }: { userId: string }) {
  const [user, setUser] = useState(null);
  
  useEffect(() => {
    fetch(`/api/users/${userId}`)
      .then(r => r.json())
      .then(setUser);
  }, [userId]);
  
  return (
    <View>
      <Image 
        source={{ uri: user?.avatar }} 
        style={{ width: 200, height: 200 }} // Unoptimized!
      />
      <Text>{user?.name}</Text>
    </View>
  );
}
```

#### Post-Vibe Cleanup Priorities

**Stage 1: Performance** (Tool: Cursor Chat)
```typescript
import { Image } from 'expo-image'; // Optimized image component

function UserProfile({ userId }: { userId: string }) {
  const [user, setUser] = useState<User | null>(null);
  
  return (
    <View>
      <Image 
        source={{ uri: user?.avatar }}
        style={{ width: 200, height: 200 }}
        contentFit="cover"
        transition={200}
        cachePolicy="memory-disk" // Proper caching
      />
      <Text>{user?.name}</Text>
    </View>
  );
}
```

**Stage 2: Platform-Specific** (Tool: Gemini)
```typescript
import { Platform } from 'react-native';

const styles = StyleSheet.create({
  container: {
    padding: Platform.select({
      ios: 20,
      android: 16,
    }),
    ...Platform.select({
      ios: {
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.25,
      },
      android: {
        elevation: 4,
      },
    }),
  },
});
```

**Cleanup Checklist:**
- [ ] Images optimized (expo-image)
- [ ] Platform-specific code handled
- [ ] Navigation memory leaks fixed
- [ ] Loading states on both platforms
- [ ] Offline support (if needed)
- [ ] Tested on real devices

---

## Python Stacks

### FastAPI + SQLAlchemy

**Ideal for:** ML APIs, data services, rapid prototyping

#### Vibe Mode Characteristics

**Speed boosters:**
- ✅ Python = super fast iteration
- ✅ Type hints = good AI suggestions
- ✅ FastAPI auto-docs = easy testing

**Common vibe outputs:**
- No async/await consistency
- N+1 queries
- Missing Pydantic validation
- Synchronous DB calls blocking
- No proper exception handling

#### Vibe Workflow

```python
# VIBE: Quick endpoint
@app.get("/users/{user_id}")
def get_user(user_id: int):
    user = db.query(User).filter(User.id == user_id).first()  # Sync!
    return user

@app.post("/users")
def create_user(name: str, email: str):  # No validation!
    user = User(name=name, email=email)
    db.add(user)
    db.commit()
    return user
```

#### Post-Vibe Cleanup Priorities

**Stage 1: Async + Validation** (Tool: Cursor Chat)
```python
from pydantic import BaseModel, EmailStr

class UserCreate(BaseModel):
    name: str
    email: EmailStr

class UserResponse(BaseModel):
    id: int
    name: str
    email: str
    
    class Config:
        from_attributes = True

@app.get("/users/{user_id}", response_model=UserResponse)
async def get_user(user_id: int):
    user = await db.get(User, user_id)
    if not user:
        raise HTTPException(status_code=404, detail="User not found")
    return user

@app.post("/users", response_model=UserResponse)
async def create_user(user: UserCreate):
    db_user = User(**user.model_dump())
    db.add(db_user)
    await db.commit()
    await db.refresh(db_user)
    return db_user
```

**Stage 2: Query Optimization** (Tool: Gemini)
```python
# Use eager loading to avoid N+1
@app.get("/users/{user_id}/posts")
async def get_user_posts(user_id: int):
    result = await db.execute(
        select(User)
        .options(selectinload(User.posts))
        .where(User.id == user_id)
    )
    user = result.scalar_one_or_none()
    if not user:
        raise HTTPException(status_code=404)
    return user.posts
```

**Cleanup Checklist:**
- [ ] All endpoints async
- [ ] Pydantic models for validation
- [ ] Proper exception handling
- [ ] Query optimization (no N+1)
- [ ] Response models defined
- [ ] Database transactions handled
- [ ] Migrations created (Alembic)

---

## Cross-Stack Vibe Patterns

### Pattern 1: "Log Everything" Vibe
```
During vibe: console.log / print / cout everywhere
After vibe: Replace with proper logging library
```

### Pattern 2: "Hardcode It" Vibe
```
During vibe: API keys, URLs, magic numbers in code
After vibe: Move to environment variables / config
```

### Pattern 3: "Copy-Paste" Vibe
```
During vibe: Duplicate code blocks liberally
After vibe: Extract to functions/components
```

### Pattern 4: "Any/Unknown" Vibe
```
During vibe: Type as any/unknown to bypass compiler
After vibe: Add proper types
```

### Pattern 5: "Inline Everything" Vibe
```
During vibe: All logic in one function/component
After vibe: Separate concerns
```

---

## Universal Cleanup Schedule

**Regardless of stack:**

| Time | Action | Tool |
|------|--------|------|
| Immediate | Commit + notes | Git |
| +15 min | Does it work? | Cline / Tests |
| +1 hour | Basic structure | Cursor Composer |
| +2 hours | Apply standards | Gemini |
| +3 hours | Documentation | Manual + AI |

---

## Stack Selection Guide

**Choose your vibe stack based on:**

| Goal | Best Stack | Why |
|------|-----------|-----|
| UI prototype | React + Tailwind | Fastest visual feedback |
| API prototype | FastAPI / Express | Quick endpoints, easy testing |
| Mobile app | React Native + Expo | Cross-platform, hot reload |
| Performance | Rust / C++ | Compiler catches issues early |
| Full-stack | Next.js | Server + client in one |
| Data processing | Python | Rich ecosystem, fast iteration |
| Audio/DSP | C++/JUCE | Real-time performance |

---

## Final Wisdom

**Stack doesn't matter for vibe coding success.**

What matters:
1. **Know your stack's footguns** - Each has unique dangers
2. **Use the right AI tool** - Different stages need different tools
3. **Cleanup is systematic** - Follow the stages
4. **Ship regularly** - Don't accumulate infinite debt

**Remember:** The best code is code that ships. Vibe boldly, clean systematically, ship confidently.

Happy vibing across all your stacks! 🎵🚀


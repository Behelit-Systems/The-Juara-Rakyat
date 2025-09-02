# 🔥 Contributing to Juara Rakyat Combat System

First, **THANK YOU** for joining the fight against scammers! 🙏

## 🎯 Mission Alignment

Before contributing, understand our mission:
- This is an **OFFENSIVE** weapon system, not a defensive tool
- We **ACTIVELY HUNT** scammers, not passively detect them
- We aim to **DESTROY** scammer operations permanently
- Every line of code should **increase scammer suffering**

## 💀 Priority Contributions

### CRITICAL NEEDS
1. **New Attack Vectors** - Creative ways to waste scammer resources
2. **Honeypot Personas** - Malaysian-specific believable characters
3. **OSINT Tools** - Track scammers across platforms
4. **Automation** - Scale operations without human intervention
5. **Legal Documentation** - Ensure we stay within the law

### Weapon Development Areas

#### 🎯 Counter-Intelligence
- Scammer identification algorithms
- Network mapping tools
- Behavioral prediction models
- Cross-platform correlation

#### 🍯 Honeypot Systems
- New persona types
- Conversation AI improvements
- Cultural authenticity
- Emotional manipulation tactics

#### 💣 Resource Exhaustion
- Time-wasting algorithms
- Psychological operations
- Channel flooding techniques
- Confusion generators

#### 📊 Analytics
- Damage assessment metrics
- Success rate tracking
- Scammer behavior analysis
- Campaign effectiveness

## 🛠️ Development Process

### 1. Choose Your Weapon
```bash
# Check available tasks
git issues --label "weapon-needed"

# Or create new weapon proposal
git issue create --template weapon-proposal
```

### 2. Set Up Combat Environment
```bash
# Fork & clone
git clone https://github.com/YOUR_USERNAME/the-juara-rakyat
cd juara-rakyat

# Create weapon branch
git checkout -b weapon/devastating-new-feature

# Install dependencies
make setup

# Start development
make dev
```

### 3. Build Your Weapon
Follow our combat standards:

#### Code Style
```javascript
// GOOD: Clear destruction intent
async function exhaustScammerResources(target) {
  const bots = await deployTimewasters(target, 100);
  await floodChannels(target);
  return calculateDamage(bots);
}

// BAD: Unclear purpose
async function processUser(u) {
  // What does this do?
}
```

#### Testing Requirements
```javascript
describe('Honeypot Trap', () => {
  it('should waste minimum 30 minutes of scammer time', async () => {
    const result = await honeypot.engage(scammer);
    expect(result.timeWasted).toBeGreaterThan(1800); // seconds
  });
  
  it('should extract intelligence during engagement', async () => {
    const intel = await honeypot.extractIntel(scammer);
    expect(intel).toHaveProperty('phoneNumbers');
    expect(intel).toHaveProperty('bankAccounts');
  });
});
```

### 4. Test Your Weapon
```bash
# Unit tests
npm test

# Integration tests
make test-integration

# Live fire test (sandbox)
make test-combat TARGET=test-scammer
```

### 5. Document Combat Effectiveness
```markdown
## Weapon: [Name]

### Damage Potential
- Time wasted: X hours per deployment
- Resources consumed: Y units
- Success rate: Z%

### Deployment
```bash
curl -X POST /weapons/deploy --data '{...}'
```

### Countermeasures
- Scammer detection: Low/Medium/High
- Sustainability: X hours before detection
```

### 6. Submit for Arsenal Integration
```bash
# Ensure destruction capability
npm run test:damage

# Verify legal compliance
npm run test:legal

# Submit PR
git push origin weapon/devastating-new-feature
```

Create PR with:
- [ ] Weapon description
- [ ] Damage metrics
- [ ] Test results
- [ ] Legal review
- [ ] Deployment guide

## 🎖️ Contribution Levels

### 🥉 Bronze Warrior (1-5 PRs)
- Basic weapons
- Bug fixes
- Documentation

### 🥈 Silver Hunter (6-20 PRs)
- New attack vectors
- System integrations
- Performance improvements

### 🥇 Gold Destroyer (21-50 PRs)
- Core system enhancements
- New weapon systems
- Architecture improvements

### 💎 Diamond Annihilator (50+ PRs)
- Strategic planning input
- Direct ops access
- Leadership role

## 📋 Code Standards

### Naming Conventions
```python
# Classes: CombatMode
class ScammerHunter:
    pass

# Functions: action_verb
def destroy_scammer_network():
    pass

# Constants: SCREAMING_SNAKE
MAX_DESTRUCTION_LEVEL = 9000

# Files: kebab-case
scammer-terminator.py
honeypot-swarm.js
```

### Comment Requirements
```javascript
/**
 * Deploys honeypot swarm to trap multiple scammers
 * @param {string} targetType - Type of scammer to target
 * @param {number} swarmSize - Number of honeypots (max 100)
 * @returns {Promise<SwarmResult>} Deployment result with trapped count
 * @destruction High - Wastes 50+ scammer hours
 */
async function deployHoneypotSwarm(targetType, swarmSize) {
  // Implementation
}
```

### Commit Messages
```bash
# Format: [type]: [description]
weapon: Add voice-based scambaiting system
enhance: Increase honeypot believability by 300%
fix: Prevent scammer detection of bot behavior
ops: Deploy 50 new elderly personas
intel: Add bank account extraction pattern
```

Types:
- `weapon`: New offensive capability
- `enhance`: Improve existing weapon
- `fix`: Bug fix
- `ops`: Operational change
- `intel`: Intelligence gathering
- `legal`: Compliance update

## 🧪 Testing Requirements

### Minimum Coverage
- Unit tests: 80%
- Integration tests: 60%
- Damage tests: REQUIRED

### Damage Test Example
```python
@pytest.mark.damage
def test_resource_exhaustion():
    """Verify weapon causes sufficient damage"""
    scammer = create_test_scammer()
    weapon = ResourceExhauster()
    
    result = weapon.attack(scammer)
    
    assert result.time_wasted > 3600  # 1 hour minimum
    assert result.messages_sent > 1000
    assert result.confusion_level == "maximum"
```

## 🚫 Unacceptable Contributions

We will **REJECT**:
- Defensive-only features
- Scammer-helping tools
- Privacy-violating code
- Illegal attack methods
- Weak weapons (<30min waste)
- Untested code

## 🎯 Bounty Program

Special rewards for:
- 🏆 New persona type that traps 10+ scammers: Recognition
- 🏆 Attack vector that wastes 100+ hours: Hall of Fame
- 🏆 Intelligence tool that maps full syndicate: Ops Access
- 🏆 Legal framework for new country: Expansion Lead


## ⚖️ Legal Requirements

All contributions must:
1. Comply with Malaysian law
2. Include legal review for new attack vectors
3. Document evidence collection standards
4. Avoid unauthorized access methods
5. Include disclaimer where appropriate

## 🎖️ Recognition

Contributors will be:
- Listed in [WARRIORS.md](WARRIORS.md)
- Credited in release notes
- Invited to Ops planning (Gold+)
- Given production access (Diamond)

---

**TOGETHER WE FIGHT. TOGETHER WE WIN.**

---

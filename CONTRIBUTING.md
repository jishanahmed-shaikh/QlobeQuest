<div align="center">

  # 🤝 Contributing to QlobeQuest
</div>

<div align="center">

![Contributing Banner](https://via.placeholder.com/800x200/4A90E2/FFFFFF?text=Welcome+Contributors!)

**Thank you for your interest in contributing to QlobeQuest! 🌍**  
*Every contribution helps connect people with global cultures*

[![Contributors](https://img.shields.io/github/contributors/jishanahmed-shaikh/QlobeQuest?style=for-the-badge)](https://github.com/jishanahmed-shaikh/QlobeQuest/graphs/contributors)
[![Pull Requests](https://img.shields.io/github/issues-pr/jishanahmed-shaikh/QlobeQuest?style=for-the-badge)](https://github.com/jishanahmed-shaikh/QlobeQuest/pulls)
[![Good First Issues](https://img.shields.io/github/issues/jishanahmed-shaikh/QlobeQuest/good%20first%20issue?style=for-the-badge)](https://github.com/jishanahmed-shaikh/QlobeQuest/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)

</div>

---

## 🌟 Ways to Contribute

### 🔧 Code Contributions

- **Frontend Development**: React/TypeScript components and features
- **Backend Development**: Node.js APIs and database optimization
- **AI Integration**: Improve Qloo and OpenAI implementations
- **Performance**: Optimization and caching improvements
- **Testing**: Unit tests, integration tests, and E2E testing

### 🎨 Non-Code Contributions

- **🌍 Cultural Content**: Authentic regional insights and recommendations
- **📝 Documentation**: Technical guides, tutorials, and API docs
- **🎨 Design**: UI/UX improvements and accessibility enhancements
- **🐛 Bug Reports**: Detailed issue reporting and reproduction steps
- **💡 Feature Requests**: Ideas for new functionality and improvements

---

## 🚀 Getting Started

### 📋 Prerequisites

Before contributing, ensure you have:

```bash
# Required Software
Node.js >= 18.0.0
npm >= 8.0.0
Git >= 2.30.0
MongoDB >= 6.0 (or Docker)
Redis >= 7.0 (or Docker)

# Recommended Tools
VS Code with extensions:
- TypeScript and JavaScript Language Features
- ESLint
- Prettier
- GitLens
```

### 🛠️ Development Setup

1. **Fork & Clone the Repository**

```bash
# Fork the repo on GitHub, then clone your fork
git clone https://github.com/YOUR_USERNAME/QlobeQuest.git
cd QlobeQuest

# Add upstream remote
git remote add upstream https://github.com/jishanahmed-shaikh/QlobeQuest.git
```

2. **Install Dependencies**

```bash
# Install all project dependencies
npm install

# Install development tools globally (optional)
npm install -g typescript ts-node nodemon
```

3. **Environment Setup**

```bash
# Copy environment template
cp .env.example .env.local

# Add your API keys (see Environment Variables section)
# QLOO_API_KEY=your_key_here
# OPENAI_API_KEY=your_key_here
```

4. **Database Setup**

```bash
# Option 1: Local MongoDB & Redis
brew install mongodb redis  # macOS
# or
sudo apt install mongodb redis  # Ubuntu

# Option 2: Docker (Recommended)
docker-compose up -d mongodb redis
```

5. **Start Development Servers**

```bash
# Terminal 1: Backend server
npm run dev:backend

# Terminal 2: Frontend server  
npm run dev:frontend

# Terminal 3: Database services (if using Docker)
docker-compose up mongodb redis
```

6. **Verify Setup**

```bash
# Run health checks
npm run health-check

# Run tests
npm test

# Open browser to http://localhost:3000
```

---

## 🔑 Environment Variables

### Required API Keys

```bash
# Qloo Taste AI (Required for cultural recommendations)
QLOO_API_KEY=your_qloo_api_key
# Get yours at: https://qloo.com/developers

# OpenAI GPT-4 (Required for narrative generation)
OPENAI_API_KEY=your_openai_api_key  
# Get yours at: https://platform.openai.com/api-keys

# Database Connections
MONGODB_URI=mongodb://localhost:27017/qlobequest
REDIS_URL=redis://localhost:6379

# Security
JWT_SECRET=your-super-secret-jwt-key-min-32-chars
ENCRYPTION_KEY=your-encryption-key-exactly-32-chars

# Optional: Development Tools
SENTRY_DSN=your_sentry_dsn_for_error_tracking
DATADOG_API_KEY=your_datadog_key_for_monitoring
```

### 🆓 Getting Free API Keys

**Qloo API (Free Tier Available)**

1. Visit [Qloo Developer Portal](https://qloo.com/developers)
2. Sign up for a free account
3. Create a new application
4. Copy your API key

**OpenAI API (Pay-per-use)**

1. Visit [OpenAI Platform](https://platform.openai.com)
2. Create an account and add billing info
3. Generate an API key
4. Start with $5 credit (usually sufficient for development)

---

## 📝 Development Workflow

### 🌿 Branch Naming Convention

```bash
# Feature branches
feature/interactive-map-improvements
feature/cultural-insights-api

# Bug fixes
fix/map-loading-performance
fix/authentication-token-refresh

# Documentation
docs/api-reference-update
docs/contributing-guide-enhancement

# Refactoring
refactor/gamification-engine-cleanup
refactor/database-query-optimization
```

### 💻 Coding Standards

#### TypeScript/JavaScript

```typescript
// ✅ Good: Use descriptive names and proper typing
interface CulturalRecommendation {
  id: string;
  name: string;
  category: CulturalCategory;
  affinityScore: number;
  region: GeographicRegion;
}

const fetchCulturalData = async (
  coordinates: LatLng,
  options: FetchOptions = {}
): Promise<CulturalRecommendation[]> => {
  // Implementation with proper error handling
  try {
    const response = await qloo.getCulturalAffinities(coordinates, options);
    return response.data.map(transformToRecommendation);
  } catch (error) {
    logger.error('Failed to fetch cultural data', { coordinates, error });
    throw new CulturalDataError('Unable to load cultural recommendations');
  }
};

// ❌ Avoid: Unclear names and missing types
const getData = async (coords: any) => {
  const data = await fetch('/api/data');
  return data.json();
};
```

#### React Components

```tsx
// ✅ Good: Proper component structure
interface CulturalMapProps {
  initialRegion: GeographicRegion;
  onRegionSelect: (region: GeographicRegion) => void;
  className?: string;
}

export const CulturalMap: React.FC<CulturalMapProps> = ({
  initialRegion,
  onRegionSelect,
  className = ''
}) => {
  const [selectedRegion, setSelectedRegion] = useState<GeographicRegion | null>(null);
  const [isLoading, setIsLoading] = useState(false);

  const handleRegionClick = useCallback(async (region: GeographicRegion) => {
    setIsLoading(true);
    try {
      await onRegionSelect(region);
      setSelectedRegion(region);
    } catch (error) {
      // Handle error appropriately
    } finally {
      setIsLoading(false);
    }
  }, [onRegionSelect]);

  return (
    <div className={`cultural-map ${className}`}>
      {/* Component implementation */}
    </div>
  );
};
```

### 🧪 Testing Requirements

#### Unit Tests (Required for all new features)

```typescript
// Example: Cultural data service test
describe('CulturalDataService', () => {
  let service: CulturalDataService;
  let mockQlooClient: jest.Mocked<QlooClient>;

  beforeEach(() => {
    mockQlooClient = createMockQlooClient();
    service = new CulturalDataService(mockQlooClient);
  });

  describe('getCulturalRecommendations', () => {
    it('should return formatted recommendations for valid coordinates', async () => {
      // Arrange
      const coordinates = { lat: 40.7128, lng: -74.0060 }; // NYC
      const mockResponse = createMockQlooResponse();
      mockQlooClient.getAffinities.mockResolvedValue(mockResponse);

      // Act
      const result = await service.getCulturalRecommendations(coordinates);

      // Assert
      expect(result).toHaveLength(5);
      expect(result[0]).toMatchObject({
        id: expect.any(String),
        name: expect.any(String),
        category: expect.any(String),
        affinityScore: expect.any(Number)
      });
    });

    it('should handle API errors gracefully', async () => {
      // Test error handling
    });
  });
});
```

#### Integration Tests

```typescript
// Example: API endpoint test
describe('Cultural Insights API', () => {
  it('should return cultural data for valid coordinates', async () => {
    const response = await request(app)
      .post('/api/cultural-insights')
      .send({
        latitude: 48.8566,
        longitude: 2.3522,
        radius: 10
      })
      .expect(200);

    expect(response.body).toMatchObject({
      recommendations: expect.any(Array),
      region: expect.any(String),
      totalCount: expect.any(Number)
    });
  });
});
```

### 📊 Performance Guidelines

#### Frontend Performance

- **Bundle Size**: Keep individual chunks under 250KB
- **Lazy Loading**: Use React.lazy() for route-based code splitting
- **Image Optimization**: Use WebP format with fallbacks
- **Caching**: Implement proper cache headers and service workers

```typescript
// ✅ Good: Lazy loading and performance optimization
const CulturalMap = React.lazy(() => import('./components/CulturalMap'));
const QuestDashboard = React.lazy(() => import('./components/QuestDashboard'));

// Preload critical components
const preloadCriticalComponents = () => {
  import('./components/CulturalMap');
  import('./components/UserProfile');
};
```

#### Backend Performance

- **Database Queries**: Use indexes and avoid N+1 queries
- **API Response Time**: Target < 200ms for data endpoints
- **Caching**: Implement Redis caching for expensive operations
- **Rate Limiting**: Protect APIs with appropriate rate limits

```typescript
// ✅ Good: Efficient database queries with caching
class CulturalDataRepository {
  async getCulturalInsights(region: string): Promise<CulturalInsight[]> {
    // Check cache first
    const cached = await this.redis.get(`cultural:${region}`);
    if (cached) {
      return JSON.parse(cached);
    }

    // Efficient database query with proper indexing
    const insights = await this.db.collection('cultural_insights')
      .find({ region })
      .sort({ affinityScore: -1 })
      .limit(20)
      .toArray();

    // Cache for 1 hour
    await this.redis.setex(`cultural:${region}`, 3600, JSON.stringify(insights));
    
    return insights;
  }
}
```

---

## 🎯 Contribution Types & Guidelines

### 🐛 Bug Reports

When reporting bugs, please include:

```markdown
## Bug Description
Clear description of what went wrong

## Steps to Reproduce
1. Go to '...'
2. Click on '....'
3. Scroll down to '....'
4. See error

## Expected Behavior
What should have happened

## Actual Behavior
What actually happened

## Environment
- OS: [e.g. macOS 13.0]
- Browser: [e.g. Chrome 108]
- Node.js version: [e.g. 18.12.0]
- QlobeQuest version: [e.g. 1.2.3]

## Additional Context
Screenshots, console logs, etc.
```

### 💡 Feature Requests

For new features, please provide:

```markdown
## Feature Summary
Brief description of the proposed feature

## Problem Statement
What problem does this solve?

## Proposed Solution
How should this feature work?

## Alternative Solutions
Other approaches considered

## Cultural Considerations
How does this respect cultural diversity and sensitivity?

## Technical Considerations
Any technical constraints or requirements
```

### 🌍 Cultural Content Guidelines

When contributing cultural content:

#### ✅ Do

- **Research thoroughly** from multiple reliable sources
- **Respect cultural nuances** and avoid generalizations
- **Include diverse perspectives** within each culture
- **Cite sources** for historical and cultural facts
- **Use inclusive language** that welcomes all users
- **Collaborate with cultural consultants** when possible

#### ❌ Don't

- **Perpetuate stereotypes** or oversimplified representations
- **Make assumptions** about cultural practices
- **Use outdated information** without verification
- **Ignore regional variations** within cultures
- **Copy content** without proper attribution

#### Example: Good Cultural Content

```typescript
// ✅ Good: Nuanced, respectful cultural insight
const culturalInsight = {
  region: "Tuscany, Italy",
  category: "food",
  title: "The Art of Tuscan Bread Making",
  description: `Tuscan bread, known as "pane sciocco" (unsalted bread), reflects the region's 
    historical relationship with salt taxes. This tradition, dating back to the 12th century, 
    has evolved into a distinctive culinary identity. Modern Tuscan bakers continue this 
    practice, pairing the bread with flavorful local ingredients like olive oil, tomatoes, 
    and cured meats.`,
  culturalContext: {
    historicalBackground: "Salt tax resistance in medieval times",
    modernRelevance: "Sustainable local food practices",
    regionalVariations: ["Pisa style", "Florence style", "Siena style"]
  },
  sources: [
    "Tuscan Culinary Institute",
    "Historical Archives of Florence",
    "Local baker interviews (2023)"
  ]
};
```

---

## 🔍 Code Review Process

### 📋 Review Checklist

Before submitting a PR, ensure:

#### Functionality

- [ ] Feature works as described in requirements
- [ ] Edge cases are handled appropriately
- [ ] Error handling is implemented
- [ ] Performance impact is acceptable

#### Code Quality

- [ ] Code follows project style guidelines
- [ ] TypeScript types are properly defined
- [ ] Functions are well-documented with JSDoc
- [ ] No console.log statements in production code
- [ ] Proper error handling and logging

#### Testing

- [ ] Unit tests cover new functionality
- [ ] Integration tests pass
- [ ] Manual testing completed
- [ ] No regression in existing features

#### Cultural Sensitivity

- [ ] Content is culturally accurate and respectful
- [ ] No stereotypes or generalizations
- [ ] Inclusive language used throughout
- [ ] Sources cited for cultural information

### 🔄 Review Process

1. **Automated Checks**: CI/CD pipeline runs tests and linting
2. **Peer Review**: At least one team member reviews code
3. **Cultural Review**: Cultural consultants review content changes
4. **Final Approval**: Maintainer approves and merges

---

## 🏆 Recognition & Rewards

### 🌟 Contributor Levels

#### 🥉 Bronze Contributors (5-20 PRs)

- Name in contributors list
- Special Discord role
- Early access to beta features

#### 🥈 Silver Contributors (20-50 PRs)

- Featured on project website
- QlobeQuest sticker pack
- Direct line to maintainers

#### 🥇 Gold Contributors (50+ PRs)

- Hall of Fame recognition
- Exclusive QlobeQuest merchandise
- Invitation to annual contributor summit
- Input on project roadmap

### 🎁 Special Recognition

- **🌍 Cultural Ambassador**: Outstanding cultural content contributions
- **🔧 Technical Innovator**: Significant technical improvements
- **📚 Documentation Hero**: Exceptional documentation contributions
- **🐛 Bug Hunter**: Consistent high-quality bug reports and fixes

---

## 📞 Getting Help

### 💬 Community Support

- **Discord**: [Connect @](https://discord.com/users/518476056232198171) for real-time help
- **GitHub Discussions**: [Ask questions](https://github.com/jishanahmed-shaikh/QlobeQuest/discussions)

### 📧 Direct Contact

- **Project Maintainer**: [Jishanahmed AR Shaikh](https://github.com/jishanahmed-shaikh) - Primary contact for project direction
- **Technical Issues**: <shaikhjishan255@gmail.com>

---

## 📜 Code of Conduct

### 🤝 Our Commitment

We are committed to providing a welcoming, inclusive environment for all contributors, regardless of:

- Background, identity, or experience level
- Geographic location or cultural background
- Technical expertise or familiarity with the project

### 🌟 Expected Behavior

- **Be respectful** in all interactions
- **Be inclusive** and welcoming to newcomers
- **Be constructive** in feedback and discussions
- **Be patient** with those learning
- **Be culturally sensitive** in all content and discussions

### 🚫 Unacceptable Behavior

- Harassment, discrimination, or exclusionary behavior
- Cultural insensitivity or stereotyping
- Trolling, insulting, or derogatory comments
- Publishing private information without consent
- Any behavior that would be inappropriate in a professional setting

### 📞 Reporting Issues

If you experience or witness unacceptable behavior:

- **Email**: <shaikhjishan255@gmail.com>

All reports will be handled confidentially and promptly.

---

<div align="center">

## 🎉 Ready to Contribute?

**Thank you for helping make QlobeQuest a platform that celebrates global cultures! 🌍**

[![Start Contributing](https://img.shields.io/badge/Start-Contributing-success?style=for-the-badge&logo=github)](https://github.com/jishanahmed-shaikh/QlobeQuest/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)
[![Join Discord](https://img.shields.io/badge/Join-Discord-7289da?style=for-the-badge&logo=discord)](https://discord.com/users/518476056232198171)

*Every contribution, no matter how small, makes a difference in connecting people with cultures worldwide.*

---

**© 2025 QlobeQuest by [Jishanahmed AR Shaikh](https://github.com/jishanahmed-shaikh) & Contributors. Made with ❤️ for cultural exploration.**


</div>

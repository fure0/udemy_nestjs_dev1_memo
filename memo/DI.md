### ❌ 直接生成する場合（結合度が高い／テスト困難）

```typescript
class UserRepository {
  findAll() { return ['Kim', 'Lee']; }
}

class UserService {
  private repo = new UserRepository(); // 自分で生成している

  getUsers() {
    return this.repo.findAll();
  }
}

// モックを使いたい場合…
class MockUserRepository {
  findAll() { return ['TestUser']; }
}

const service = new UserService();
// ❌ UserService の中で UserRepository が固定されている → Mock に差し替え不可
console.log(service.getUsers()); // ['Kim', 'Lee']
```

### ✅ 外部から注入（結合度が低い／テストしやすい）
```typescript
class UserRepository {
  findAll() { return ['Kim', 'Lee']; }
}

class UserService {
  constructor(private repo: { findAll: () => string[] }) {} // インターフェースに依存

  getUsers() {
    return this.repo.findAll();
  }
}

// 実際の利用
const realRepo = new UserRepository();
const service = new UserService(realRepo);
console.log(service.getUsers()); // ['Kim', 'Lee']

// テスト時にモックを注入
const mockRepo = { findAll: () => ['TestUser'] };
const testService = new UserService(mockRepo);
console.log(testService.getUsers()); // ['TestUser']

```
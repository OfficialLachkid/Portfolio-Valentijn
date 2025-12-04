# Code Conventions Documentation

## 1. Analyze

Before establishing our code conventions, it's essential to assess common mistakes and align our practices with industry standards. Particularly those related to Unity development, C# guidelines, and GitLab workflows.

### Current Challenges
- Inconsistent naming conventions cause confusion and increase the risk of errors.
- Vague or excessive comments hinder understanding of complex logic.
- Lack of structured code reviews leads to merge conflicts and miscommunication.

### Goals
- Adopt naming standards aligned with Microsoft’s .NET Capitalization Conventions.
- Improve comment clarity following guidance such as Stack Overflow’s best practices.
- Streamline GitLab review workflows to ensure maintainability and high-quality code.

---

## 2. Advise

### Naming Conventions
- **PascalCase** for public types: classes, properties, and methods.
  ```csharp
  public class RamanSpectrometer {}
  public void StartMeasurement() {}
  ```
- **camelCase** for private variables and method parameters.
  ```csharp
  private int _measurementCount = 5;
  private void UpdateStatus(string statusMessage) {}
  ```
- Use meaningful and descriptive names. Avoid abbreviations unless widely recognized.

> 💡 **Tip:** Meaningful names reduce time spent debugging.

---

### Code Commenting Standards
- Add XML-style summary comments to all public classes and methods:
  ```csharp
  /// <summary>
  /// Starts the measurement process for the spectrometer.
  /// </summary>
  public void StartMeasurement() {}
  ```
- Use inline comments only for complex logic.
- Avoid redundant comments.

> ℹ️ **Info:** Good comments explain *why*, not *what*.

---

### GitLab Workflow
- Use branching strategy: `feature/my-new-feature`
- All changes require merge requests.
- Assign at least two reviewers.
- Use "Resolve Thread" to track resolved discussions.

---

### Unity-Specific Guidelines
- Organize scripts logically (Scripts/Player, Scripts/Environment).
- Avoid hardcoded values: use ScriptableObjects or config files.
- Use Managers to centralize logic for large features.

---

## 3. Design

### Code Standards Documentation
- Create a shared standards document in the repository.
- Include examples and visuals.

### Review Workflow in GitLab
Reviewers must check for:
- Naming and commenting consistency
- Functionality correctness
- Unity-specific conventions

### Linter Integration
Add a C# linter to GitLab CI.

**Example**
**Before:**
```csharp
void DoSomething() { int a = 0; /* Logic */ }
```

**After:**
```csharp
/// <summary>
/// Initializes the player movement with default settings.
/// </summary>
public void InitializeMovement()
{
    int initialSpeed = 0;
    // Logic for initialization
}
```

---

## 4. Realize

### Code Review Checklist
- ✅ Uses PascalCase for public identifiers; camelCase for private
- ✅ Clear, concise comments
- ✅ No unused code
- ✅ Follows Unity folder structure

### Unity Best Practices
- Use descriptive script names.
- Implement `OnValidate()` for editor-time validation.

### Automated Tools
Add linting to CI pipeline to enforce consistency.

---

## 5. Manage & Control

### Quality Assurance
- Conduct weekly team reviews.

### GitLab Metrics
- Review turnaround time
- Violations per merge request

### Continuous Improvement
- Update conventions with team feedback.
- Adjust linter settings as project scales.

### Version Control Best Practices
**Good commit example:**
```
fix: Corrected ray color update logic in Spectrometer
```
**Bad example:**
```
changed stuff
```

---

## References
- Microsoft .NET Capitalization Conventions  
- Stack Overflow Blog on Code Comments  
- C# Coding Standards and Naming Conventions  

# 🧠 MSSA Cloud App Dev Notes – C#, Docker & .NET Core

*A practical introduction to compiled languages in a modern cloud workflow*

---

### 💡 Why C# Needs a Compiler:

C# is a **compiled language**, which means the code you write (called **source code**) must be **translated into a lower-level language** before the computer can run it. This is done by the **C# compiler**, which turns your `.cs` files into **Intermediate Language (IL)**. The **.NET runtime (CLR)** then translates IL into **machine code** just-in-time (JIT), when your app runs.

> ✅ This makes C# fast, secure, and great for building enterprise-scale cloud applications.

---

### 🐳 Why Use Docker with .NET?

Docker lets you run your C#/.NET app in a **lightweight container** that works the same everywhere — on your dev machine, in Azure, or in production.

Benefits:

* 🚀 **Portability**: "Build once, run anywhere"
* 🔐 **Isolation**: Keeps dependencies clean
* 🧪 **Testability**: Run multiple versions without conflict
* 📆 **CI/CD Ready**: Plug into GitHub Actions, Azure DevOps, etc.

---

### ⚙️ Sample Dockerfile for .NET Core App

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MyApp/MyApp.csproj", "MyApp/"]
RUN dotnet restore "MyApp/MyApp.csproj"
COPY . .
WORKDIR "/src/MyApp"
RUN dotnet build "MyApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyApp.dll"]
```

---

### 🛠 Tools Used

| Tool                  | Role                    |
| --------------------- | ----------------------- |
| 🧱 **C# / .NET**      | Language + Framework    |
| 🐳 **Docker**         | Containerized runtime   |
| 🧪 **VS Code + MSSA** | Dev environment         |
| 🔙 **GitHub + Git**   | Version control & CI/CD |

---

### 📘️ Summary

> You're not just learning C# — you're learning how **modern cloud-native development** works with compiled languages, containers, and collaborative tools like GitHub. This skillset prepares you to work in **real-world cloud dev teams** where your code scales, deploys, and improves automatically.

---

### 📜 Beginner Git Cheat Sheet (for MSSA Devs)

If you're new to Git or GitHub, use this as your **starter guide**.

| 🔧 Action                   | 🧪 Git Command Example                       | 💬 What It Does                                     |
| --------------------------- | -------------------------------------------- | --------------------------------------------------- |
| ✅ Initialize Git            | `git init`                                   | Starts tracking your project with Git locally       |
| 📅 Clone a repo from GitHub | `git clone https://github.com/user/repo.git` | Downloads a copy of a remote GitHub project         |
| ➕ Stage changes             | `git add .` or `git add MyFile.cs`           | Prepares changes to be committed                    |
| 📂 Commit changes           | `git commit -m "Add login feature"`          | Saves a version snapshot with a message             |
| 🚀 Push to GitHub           | `git push origin main`                       | Uploads your local commits to GitHub                |
| 🔄 Pull from GitHub         | `git pull origin main`                       | Gets the latest changes from the remote GitHub repo |
| 🔍 Check status             | `git status`                                 | Shows which files have been changed or staged       |
| 📜 View commit history      | `git log --oneline`                          | Displays a clean list of past commits               |
| ✨ Create a new branch       | `git checkout -b feature/new-ui`             | Starts a new branch for isolated development        |
| ↺ Merge a branch            | `git merge feature/new-ui`                   | Combines a branch into the current one              |

> 👇 Pro Tip: Always commit small and often. It's easier to track and rollback changes if needed.

---

Would you like me to:

* Add GitHub Actions YAML for .NET CI/CD?
* Include a `.gitignore` file tailored for C# and Docker?
* Create a markdown printable version of the cheat sheet?

Just say the word, and I’ll get it ready.

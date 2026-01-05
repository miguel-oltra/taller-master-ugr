# Exercise Outcomes Submission Template

**Student/Group Name**: GROUP 7. García Mora, María Luisa. Mejías Real, Javier. Revaliente Casilla, Victor Manuel  
**Level Completed**: intermediate
**Date**: 5/01/2026

---

## 📋 Exercise Summary

### Exercise: Intermediate Git
**Status**: ✅ Completed 

**What I did**:
In general, we have managed to execute all the proposed git commands in practice except for the push command, which gives me a permissions error in the miguel-oltra/taller-master-ugr.git repository.

**Commands Used**:
```bash
git checkout intermediate
git checkout -b feature/header
git checkout intermediate
git checkout -b feature/footer
git add page.html
git commit -m "Add header to page"
git checkout feature/footer
git add page.html
git commit -m "Add footer to page"
git checkout intermediate
git merge feature/header
git merge feature/footer
git tag -a v1.0 -m "First stable version with merged features"
git tag
git show v1.0
git push origin v1.0 #Error por permisos#
git tag v1.0-test
git show v1.0
git show v1.0-test
```

**Results/Output**:
```
$ git commit -m "Add header to page"
Add header to page
1 file changed, 13 insertions(+)
create mode 100644 page.html

$ git commit -m "Add footer to page"
Add footer to page
1 file changed, 1 insertions(+)

$ git push origin v1.0
ERROR: Permission to miguel-oltra/taller-master-ugr.git denied to jameraguilar.
fatal: No se pudo leer del repositorio remoto.

Por favor asegúrate de que tengas los permisos de acceso correctos
y que el repositorio exista.
```

**Screenshots** (if applicable):
- [Captura 1: Seleccionamos la rama intermediate](capturas/captura1.png)
- [Captura 2: Cambiamos entre la rama header y footer ](capturas/captura2.png)
- [Captura 3: Ejemplo página html creada](capturas/captura3.png)
- [Captura 4: Distintos comandos checkout](capturas/captura4.png)
- [Captura 5: Ejemplo página html con footer](capturas/captura5.png)
- [Captura 6: Comando Add y commit con la página con pie de página](capturas/captura6.png)
- [Captura 7: Comando merge a priori todo va bien](capturas/captura7.png)
- [Captura 8: Error al hacer el push](capturas/captura8.png)


---

## 🎯 Key Learnings

**Main concepts I learned**:
1. [Concept 1,"How to switch branches and select intermediate"]
2. [Concept 2,"Add and commit operations for a web page"]
3. [Concept 3,"Use the merge command"]
4. [Concept 4,"See how a push without write permissions results in an error"]

**Skills I improved**:
- [Skill 1, "Switch branches"]
- [Skill 2, "Add HTML files and commit"]
- [Skill 3, "Conflict resolution"]

---

## 🚧 Challenges Faced

### Challenge 1: [Error writing]
**Problem**: [Error writing to the teacher's repository]

**Solution**: [Fork the repository to our account and work on it]

---

## 💭 Personal Reflection

**What surprised me**:
[Not having write permissions in the teacher's repository]

**What I found most difficult**:
[The ability to push]

**What I found most useful**:
[Learn how to use git]

**How I would apply this in real projects**:
[Teaching students how to use Git]

---

## 📊 Self-Assessment

Rate your confidence level for each topic (1-5, where 5 is very confident):

| Topic | Confidence (1-5) | Notes |
|-------|------------------|-------|
| Basic Git commands | [4] | Add/commit process fully understood. |
| Branching & merging | [4] | Parallel branch management included. |
| Remote operations | [3] | Due to the not entirely clear permissions error |
| Conflict resolution | [3] | In the process of learning |
| History rewriting | [4] | Well, but we need to practice more. |
| Git hooks | [3] | Well, but we need to practice more. |
| Security practices | [3] | Well, but we need to practice more. |

---

## 🔗 Evidence/Artifacts

**Links to branches/commits**:
- Link to your outcome branch: `https://github.com/jameraguilar/taller-master-ugr-tree-group-7-outcomes-intermediate/blob/main/OUTCOMES.md`
- Key commits demonstrating your work:
  - Commit hash: [Short description]
  - Commit hash: [Short description]


---

## ✅ Completion Checklist

Before submitting, ensure you have:
- [x] Completed the exercise for your chosen level (including all parts)
- [x] Documented all commands used with their outputs
- [x] Described challenges and how you resolved them
- [x] Provided a thoughtful reflection on your learning
- [x] Self-assessed your confidence in each topic
- [x] Pushed your outcome branch to the remote repository
- [x] Created a Pull Request (if required by your instructor)

---

## 📝 Additional Comments

[We don't know if not having writing permission was a challenge or a mistake]

---

**Submission Date**: [05/01/2026]  
**Ready for Review**: ✅ Yes 

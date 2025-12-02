# 🐳 Docker Commands vs ENTRYPOINT Lab

In this lab, I learned how to **inspect ENTRYPOINT and CMD in Dockerfiles, understand how they work together, determine final startup commands, and override defaults when running containers**.

---

## 📋 Lab Overview

**Goal:**

* Inspect Dockerfiles for ENTRYPOINT and CMD
* Understand how ENTRYPOINT + CMD combine at runtime
* Identify startup commands for MySQL, WordPress, and Ubuntu images
* Override CMD using command arguments when running containers

**Learning Outcomes:**

* Read Dockerfiles using `cat`
* Identify ENTRYPOINT scripts
* Understand how CMD and ENTRYPOINT interact
* Run containers with custom startup commands
* Use `docker run -d IMAGE COMMAND` to override CMD

---

## 🛠 Step-by-Step Journey

### **Step 1: Inspect Dockerfiles Provided in `/root`**

Dockerfiles for MySQL, WordPress, and Ubuntu are located under:

```
/root/
```

Checked them using:

```bash
ls
cat Dockerfile-mysql
cat Dockerfile-wordpress
cat Dockerfile-ubuntu
```

---

### **Step 2: Identify ENTRYPOINT for the MySQL Image**

**Command:**

```bash
cat Dockerfile-mysql
```

* ENTRYPOINT found:

```
docker-entrypoint.sh
```

---

### **Step 3: Identify CMD for the WordPress Image**

**Command:**

```bash
cat Dockerfile-wordpress
```

* CMD found:

```
apache2-foreground
```

---

### **Step 4: Determine the Final Startup Command for WordPress**

WordPress image has:

* ENTRYPOINT = `docker-entrypoint.sh`
* CMD = `apache2-foreground`

Therefore, the final combined startup command is:

```
docker-entrypoint.sh apache2-foreground
```

✔️ ENTRYPOINT is the executable
✔️ CMD is the default argument

---

### **Step 5: Determine Ubuntu Startup Command**

**Command:**

```bash
cat Dockerfile-ubuntu
```

* CMD found:

```
bash
```

Final startup command when Ubuntu runs:

```
bash
```

(No ENTRYPOINT, so CMD runs directly.)

---

### **Step 6: Run Ubuntu With a Custom Startup Command (`sleep 1000`)**

Task:
Run Ubuntu in *detached mode*, overriding the default CMD.

**Command:**

```bash
docker run -d ubuntu sleep 1000
```

✔️ Overrides CMD
✔️ Runs in background
✔️ Container is now sleeping for 1000 seconds

---

## ✅ Key Commands Summary

| Task                            | Command / Notes                   |
| ------------------------------- | --------------------------------- |
| View Dockerfiles                | `cat Dockerfile-name`             |
| Inspect ENTRYPOINT              | `ENTRYPOINT ["script.sh"]`        |
| Inspect CMD                     | `CMD ["command"]`                 |
| Determine final startup command | ENTRYPOINT + CMD                  |
| Override CMD                    | `docker run IMAGE custom-command` |
| Run container detached          | `docker run -d IMAGE`             |

---

## 💡 Notes / Tips

* **ENTRYPOINT** is the *main executable*
* **CMD** provides *default arguments*
* Final runtime command = **ENTRYPOINT + CMD**
* To override CMD, simply append a command after the image name
* To override ENTRYPOINT, use `--entrypoint`
* WordPress and MySQL rely heavily on ENTRYPOINT scripts for initialization

---

## 📌 Lab Summary

| Step                                  | Status | Key Takeaways                                        |
| ------------------------------------- | ------ | ---------------------------------------------------- |
| Inspect Dockerfiles                   | ✅      | Found MySQL, WordPress, Ubuntu configs               |
| MySQL ENTRYPOINT                      | ✅      | `docker-entrypoint.sh`                               |
| WordPress CMD                         | ✅      | `apache2-foreground`                                 |
| Final WordPress startup command       | ✅      | `docker-entrypoint.sh apache2-foreground`            |
| Ubuntu startup command                | ✅      | CMD = `bash`                                         |
| Override Ubuntu CMD with `sleep 1000` | ✅      | Ran detached using `docker run -d ubuntu sleep 1000` |

---

## ✅ References

* [ENTRYPOINT vs CMD (Docker Docs)](https://docs.docker.com/engine/reference/builder/#entrypoint)
* [How Docker Runs Commands](https://docs.docker.com/engine/reference/run/)
* [Best Practices for Dockerfile](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

# 🧩 Kubernetes Admission Controllers

A focused walkthrough showing how **Admission Controllers** influence Kubernetes API behavior — specifically, how enabling or disabling certain controllers affects object creation and validation.

---

## 🔍 Step 1 – Checking Enabled Admission Controllers

**We start by checking which admission controllers are currently enabled by default in our cluster.**

<br><br>

<p align="center">
  <img width="1075" height="325" alt="enabled admission controllers" src="https://github.com/user-attachments/assets/fa616ff7-a72d-42e0-8e98-aa7c57380b9c" />
</p>

<br><br>

---

## 🧾 Step 2 – Reviewing the API Server Manifest

**To view non-default (custom) admission controllers, we inspect the API server manifest file (`/etc/kubernetes/manifests/kube-apiserver.yaml`).**  
This file defines which admission plugins are active via the `--enable-admission-plugins` flag.

<br><br>

<p align="center">
  <img width="636" height="77" alt="api server manifest" src="https://github.com/user-attachments/assets/39042f73-37da-4d60-81f0-fa16805d4e91" />
</p>

<br><br>

---

## 🚫 Step 3 – Testing Behavior Without NamespaceAutoProvision

**Let’s attempt to create a Pod in a namespace that does not exist.**  
Since the `NamespaceAutoProvision` admission controller is *not yet enabled*, this operation should fail.

<br><br>

<p align="center">
  <img width="420" height="35" alt="pod creation fail" src="https://github.com/user-attachments/assets/2804e22d-6923-46fa-b09f-a002801ffc58" />
</p>

<br><br>

---

## ⚙️ Step 4 – Enabling the NamespaceAutoProvision Controller

**Now we edit the API server manifest and add `NamespaceAutoProvision` to the list of enabled admission plugins.**  
This controller automatically creates namespaces when an object references a non-existent one.

<br><br>

<p align="center">
  <img width="565" height="287" alt="enable namespaceautoprovision" src="https://github.com/user-attachments/assets/2c140e99-15b7-4072-a521-dbff2ed9a619" />
</p>

<br><br>

---

## ✨ Step 5 – Testing the Behavior Again

**After saving and waiting for the API server to restart, we try creating the Pod again.**  
This time, Kubernetes automatically provisions the namespace — confirming that the admission controller is working as intended.

<br><br>

<p align="center">
  <img width="442" height="38" alt="pod creation success" src="https://github.com/user-attachments/assets/be8520f3-bdb0-4942-ad10-c1e64a88bcde" />
</p>

<br><br>

---

## 🧠 Key Takeaways

- **Admission Controllers** are interceptors that modify or validate API requests before persistence.  
- They can **enforce policies**, **auto-create resources**, or **inject defaults**.  
- You can enable or disable controllers by editing the API server manifest’s `--enable-admission-plugins` flag.  
- The `NamespaceAutoProvision` plugin demonstrates how Kubernetes can dynamically create missing namespaces.  

---

<p align="center"><b>Admission Controllers are Kubernetes’ policy gatekeepers — controlling what gets admitted into the cluster API.</b></p>





Here’s a **step-by-step guide** based on your command history, so you can follow it easily in the future.  

---

# **Guide: Setting Up and Using DAGsHub with DVC**  

## **1. Create a DAGsHub Repository**
1. **Go to DAGsHub**: [https://dagshub.com](https://dagshub.com)  
2. **Click "Create +" (upper right corner)**  
3. **Set up the repository name** and create it.  

## **2. Clone the Repository Locally**  
Find the cloning commands in DAGsHub:  
1. Click the **green "Remote" button**  
2. Copy the **Git repository URL**  
3. Copy the **DVC remote setup** commands  

Then, run:  
```bash
git clone https://dagshub.com/perwaaler/hello-world.git
cd hello-world/
git status  # Verify the repo is cloned
```

---

## **3. Set Up a Python Virtual Environment (Optional, but Recommended)**
If using `pyenv`:  
```bash
pyenv virtualenv dvctutorial
```

---

## **4. Install DVC and Initialize It**
```bash
pip install dvc
dvc init
```
This creates a `.dvc` directory and sets up DVC tracking.

---

## **5. Set Up the DVC Remote (DAGsHub)**
1. **Add the DAGsHub DVC remote**  
   ```bash
   dvc remote add origin https://dagshub.com/perwaaler/hello-world.dvc
   ```
2. **Enable authentication**  
   ```bash
   dvc remote modify origin --local auth basic
   dvc remote modify origin --local user perwaaler
   ```
3. **Create a DAGsHub token**  
   - Go to [DAGsHub Tokens](https://dagshub.com/user/settings/tokens)  
   - **Generate a new token**  
   - **Store it securely** (e.g., in Bitwarden)  

4. **Set the token for authentication**  
   ```bash
   dvc remote modify origin --local password YOUR_TOKEN_HERE
   ```

---

## **6. Commit and Push the DVC Initialization to Git**
```bash
git add -A
git commit -m "Initialized DVC"
git push
```

---

## **7. Add and Track Data**
### **First Version (v0)**
```bash
mkdir data
echo "dummy data right here!" > data/dummydatav0.txt
dvc add data
git add -A
git commit -m "Added data with v0 data"
git push
dvc push -r origin data
```
This uploads the `data/` directory to DAGsHub via DVC.

---

### **Update Data to Version 1 (v1)**
```bash
echo "this is version 1 of the data (updated once)" > data/dummydatav0.txt
dvc add data
git add -A
git commit -m "Updated data to v1"
git push
dvc push -r origin data
```

---

## **Summary of Key Commands**
| **Task** | **Command** |
|----------|------------|
| Clone DAGsHub repo | `git clone <repo_url>` |
| Initialize DVC | `dvc init` |
| Add DVC remote | `dvc remote add origin <dvc_repo_url>` |
| Authenticate with DAGsHub | `dvc remote modify origin --local auth basic` |
| Set username | `dvc remote modify origin --local user <your_username>` |
| Set token (from DAGsHub settings) | `dvc remote modify origin --local password <your_token>` |
| Add and track data | `dvc add <data_folder>` |
| Push data to DAGsHub | `dvc push -r origin <data_folder>` |
| Pull data from DAGsHub | `dvc pull` |

---

### **Now You Have a Fully Functional DAGsHub + DVC Setup!**
Let me know if you need any tweaks to the guide!
# AAE5303 Environment Setup Report — Template for Students

> **Important:** Follow this structure exactly in your submission README.  
> Your goal is to demonstrate **evidence, process, problem-solving, and reflection** — not only screenshots.

---

## 1. System Information

**Laptop model:**  
My laptop is acer swift3 with i5-1135G7@4core and 16g ram and 7.72g avaliable storage, hence it is impossible for using Docker and Container in the device (I have used it before in my PC so am able to estimate the possibility and draw the conclusion). So I have to use a rented cloud service for the task, and finally select AutoDL (https://www.autodl.com/) with a instance (actually a docker container based on ubuntu22.04 and could install packages) that may fit the following tasks request with pytorch-gpu etc..

<img width="2243" height="1286" alt="image" src="https://github.com/user-attachments/assets/2c82d401-b647-4cc5-8cda-d9d25ed31de3" />

**CPU / RAM:**  
16 vCPU Intel(R) Xeon(R) Platinum 8352V CPU @ 2.10GHz / 120GB RAM

**Host OS:**  
Ubuntu 22.04

**Linux/ROS environment type:**  
_[Choose one:]_
- [ ] Dual-boot Ubuntu
- [ ] WSL2 Ubuntu
- [ ] Ubuntu in VM (UTM/VirtualBox/VMware/Parallels)
- [ ] Docker container
- [ ] Lab PC
- [x] Remote Linux server

---

## 2. Python Environment Check

### 2.1 Steps Taken

Describe briefly how you created/activated your Python environment:

**Tool used:**  
_[venv / conda / system Python]_

**Key commands you ran:**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

**Any deviations from the default instructions:**  
I used conda before with routhly steps of: 1)download anaconda or miniconda; 2)use conda prompt for the command 'conda creat -n python=xx.xx'; 3)'activate -n' the venv and install packages; 4)find the interpreter in ide and use the venv (need to add environment variable in win10, and may need a CUDA or cudatookit package)

But it is easy and enjoy for complete these complex steps by rent a cloud service, just recharge the AutoDL platform, select a instance and start, use remote ssh to connect the instant (container) in IDE (https://www.bilibili.com/video/BV1BtpEzxENN).

### 2.2 Test Results

Run these commands and paste the actual terminal output (not just screenshots):

```bash
python scripts/test_python_env.py
```

**Output:**
```
root@autodl-container-5584468052-9b2db44b:~/AAE5303/Assessment1/PolyU-AAE5303-env-smork-test# cd /root/AAE5303/Assessment1/PolyU-AAE5303-env-smork-test && source /opt/ros/humble/setup.bash && python3 scripts/test_python_env.py
========================================
AAE5303 Environment Check (Python + ROS)
Goal: help you verify your environment and understand what each check means.
========================================

Step 1: Environment snapshot
  Why: We capture platform/Python/ROS variables to diagnose common setup mistakes (especially mixed ROS env).
Step 2: Python version
  Why: The course assumes Python 3.10+; older versions often break package wheels.
Step 3: Python imports (required/optional)
  Why: Imports verify packages are installed and compatible with your Python version.
Step 4: NumPy sanity checks
  Why: We run a small linear algebra operation so success means more than just `import numpy`.
Step 5: SciPy sanity checks
  Why: We run a small FFT to confirm SciPy is functional (not just installed).
Step 6: Matplotlib backend check
  Why: We generate a tiny plot image (headless) to confirm plotting works on your system.
Step 7: OpenCV PNG decoding (subprocess)
  Why: PNG decoding uses native code; we isolate it so corruption/codec issues cannot crash the whole report.
Step 8: Open3D basic geometry + I/O (subprocess)
  Why: Open3D is a native extension; ABI mismatches can segfault. Subprocess isolation turns crashes into readable failures.
Step 9: ROS toolchain checks
  Why: The course requires ROS tooling. This check passes if ROS 2 OR ROS 1 is available (either one is acceptable).
  Action: building ROS 2 workspace package `env_check_pkg` (this may take 1-3 minutes on first run)...
  Action: running ROS 2 talker/listener for a few seconds to verify messages flow...
Step 10: Basic CLI availability
  Why: We confirm core commands exist on PATH so students can run the same commands as in the labs.

=== Summary ===
✅ Environment: {
  "platform": "Linux-5.15.0-78-generic-x86_64-with-glibc2.35",
  "python": "3.12.3",
  "executable": "/root/miniconda3/bin/python3",
  "cwd": "/root/AAE5303/Assessment1/PolyU-AAE5303-env-smork-test",
  "ros": {
    "ROS_VERSION": "2",
    "ROS_DISTRO": "humble",
    "ROS_ROOT": null,
    "ROS_PACKAGE_PATH": null,
    "AMENT_PREFIX_PATH": "/opt/ros/humble",
    "CMAKE_PREFIX_PATH": null
  }
}
✅ Python version OK: 3.12.3
✅ Module 'numpy' found (v2.1.3).
✅ Module 'scipy' found (v1.17.0).
✅ Module 'matplotlib' found (v3.9.2).
✅ Module 'cv2' found (v4.13.0).
✅ Missing optional module 'rclpy'.
✅ numpy matrix multiply OK.
✅ numpy version 2.1.3 detected.
✅ scipy FFT OK.
✅ scipy version 1.17.0 detected.
✅ matplotlib backend OK (Agg), version 3.9.2.
✅ OpenCV OK (v4.13.0), decoded sample image 128x128.
✅ Open3D OK (v0.19.0), NumPy 2.1.3.
✅ Open3D loaded sample PCD with 8 pts and completed round-trip I/O.
✅ ROS 2 CLI OK: /opt/ros/humble/bin/ros2
✅ ROS 1 tools not found (acceptable if ROS 2 is installed).
✅ colcon found: /usr/bin/colcon
✅ ROS 2 workspace build OK (env_check_pkg).
✅ ROS 2 runtime OK: talker and listener exchanged messages.
✅ Binary 'python3' found at /root/miniconda3/bin/python3

All checks passed. You are ready for AAE5303 🚀
```

```bash
python scripts/test_open3d_pointcloud.py
```

**Output:**
```
root@autodl-container-5584468052-9b2db44b:~/AAE5303/Assessment1# cd /root/AAE5303/Assessment1/PolyU-AAE5303-env-smork-test && python3 scripts/test_open3d_pointcloud.py
ℹ️ Loading /root/AAE5303/Assessment1/PolyU-AAE5303-env-smork-test/data/sample_pointcloud.pcd ...
✅ Loaded 8 points.
   • Centroid: [0.025 0.025 0.025]
   • Axis-aligned bounds: min=[0. 0. 0.], max=[0.05 0.05 0.05]
✅ Filtered point cloud kept 7 points.
✅ Wrote filtered copy with 7 points to /root/AAE5303/Assessment1/PolyU-AAE5303-env-smork-test/data/sample_pointcloud_copy.pcd
   • AABB extents: [0.05 0.05 0.05]
   • OBB  extents: [0.08164966 0.07071068 0.05773503], max dim 0.0816 m
🎉 Open3D point cloud pipeline looks good.
```

**Screenshot:**  
<img width="2256" height="1434" alt="image" src="https://github.com/user-attachments/assets/19cd6f9d-3bb1-4bed-a2f4-25ff09d97ff8" />
<img width="2256" height="1434" alt="image" src="https://github.com/user-attachments/assets/ced5725e-e9d6-4a18-ad85-6281b43568ac" />


## 3. ROS 2 Workspace Check

### 3.1 Build the workspace

Paste the build output summary (final lines only):

```bash
source /opt/ros/humble/setup.bash
colcon build
```

**Expected output:**
```
Summary: 1 package finished [x.xx s]
```

**Your actual output:**
```
3-env-smork-test# source /opt/ros/humble/setup.bash
colcon build
Starting >>> env_check_pkg
Finished <<< env_check_pkg [9.38s]                     

Summary: 1 package finished [9.63s]
```

### 3.2 Run talker and listener

Show both source commands:

```bash
source /opt/ros/humble/setup.bash
source install/setup.bash
```

**Then run talker:**
```bash
ros2 run env_check_pkg talker.py
```

**Output (3–4 lines):**
```
3-env-smork-test# ros2 run env_check_pkg talker
[INFO] [1769013842.728331552] [env_check_pkg_talker]: AAE5303 talker ready (publishing at 2 Hz).
[INFO] [1769013843.228567340] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #0'
[INFO] [1769013843.728486863] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #1'
[INFO] [1769013844.228452948] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #2'
[INFO] [1769013844.728387517] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #3'
```

**Run listener:**
```bash
ros2 run env_check_pkg listener.py
```

**Output (3–4 lines):**
```
ros2 run env_check_pkg listener
[INFO] [1769013826.100512274] [env_check_pkg_listener]: AAE5303 listener awaiting messages.
[INFO] [1769013843.228797096] [env_check_pkg_listener]: I heard: 'AAE5303 hello #0'
[INFO] [1769013843.728704861] [env_check_pkg_listener]: I heard: 'AAE5303 hello #1'
[INFO] [1769013844.228653884] [env_check_pkg_listener]: I heard: 'AAE5303 hello #2'
[INFO] [1769013844.728589750] [env_check_pkg_listener]: I heard: 'AAE5303 hello #3'
```

**Alternative (using launch file):**
```bash
ros2 launch env_check_pkg env_check.launch.py
```

**Screenshot:**  
<img width="2256" height="1434" alt="image" src="https://github.com/user-attachments/assets/044d0b8d-276c-42ae-8306-835db3f08eb3" />

<img width="2256" height="1434" alt="image" src="https://github.com/user-attachments/assets/4529b15f-3b93-46c4-8baf-876c93994e2e" />


## 4. Problems Encountered and How I Solved Them

> **Note:** Write 2–3 issues, even if small. This section is crucial — it demonstrates understanding and problem-solving.

### Issue 1: The inadequent token of free version cursor

**Cause / diagnosis:**  
The intrinsic propety of cursor

**Fix:**  
Use Taobao for a cheaper way to solve, costed 20RMB that far less than directly recharge cursor pro about 160RMB.

```bash
None
```

**Reference:**  
None

---

### Issue 2: The fail of command 'ros2 run env_check_pkg talker.py'

**Cause / diagnosis:**  
This package has two executable files: talker and listener (both compiled in C++, not Python scripts).

**Fix:**  
run:

```bash
ros2 run env_check_pkg talker
```

**Reference:**  
AI assistant.

---

### Issue 3 (Optional): Can not find the Open3d and Ros package

**Cause / diagnosis:**  
There are base env and conda env in the instance.

**Fix:**  
Use conda env.

```bash
cd /root/AAE5303/Assessment1/PolyU-AAE5303-env-smork-test
python3 scripts/test_open3d_pointcloud.py
```

**Reference:**  
AI assistant.

---

## 5. Use of Generative AI (Required)

Choose one of the issues above and document how you used AI to solve it.

> **Goal:** Show critical use of AI, not blind copying.

### 5.1 Exact prompt you asked

**Your prompt:**
```
为什么这个运行不了：ros2 run env_check_pkg listener
```

### 5.2 Key helpful part of the AI's answer

**AI's response (relevant part only):**
```
为什么看起来"没反应"？
listener 是一个订阅者，它的作用是：
等待并接收来自 talker 发布的消息
如果没有 talker 在运行，它就只是静静地等待
这是正常行为！
如何正确测试 talker 和 listener？
您需要同时运行两个程序，在两个不同的终端：
```

### 5.3 What you changed or ignored and why

Explain briefly:
- Did the AI recommend something unsafe?
- Did you modify its solution?
- Did you double-check with official docs?

**Your explanation:**  
I changed and succeed. AI did not recommend something unsafe. I did not modify its solution. I did not double-check with official docs because I know the operition is safe by my experience.

### 5.4 Final solution you applied

Show the exact command or file edit that fixed the problem:

```bash
cd /root/AAE5303/Assessment1/PolyU-AAE5303-env-smork-test
source /opt/ros/humble/setup.bash
source install/setup.bash
ros2 run env_check_pkg listener

cd /root/AAE5303/Assessment1/PolyU-AAE5303-env-smork-test
source /opt/ros/humble/setup.bash
source install/setup.bash
ros2 run env_check_pkg listener
```

**Why this worked:**  
The intrinsic propety of ros.

---

## 6. Reflection (3–5 sentences)

Short but thoughtful:

- What did you learn about configuring robotics environments?
- What surprised you?
- What would you do differently next time (backup, partitioning, reading error logs, asking better AI questions)?
- How confident do you feel about debugging ROS/Python issues now?

**Your reflection:**

1)AI, cloud service and docker is hlepful for build and manage the envs; 2)The convenience of AI in cursor that can directly check the code and terminal and system files to find the solution, even run or modify the command or code itself; 3)Change my favorite IDE to cursor; 4) Better and faster my myself.

---

## 7. Declaration

✅ **I confirm that I performed this setup myself and all screenshots/logs reflect my own environment.**

**Name:**  
XING Yiwei

**Student ID:**  
25060169g

**Date:**  
22/01/2026

---

## Submission Checklist

Before submitting, ensure you have:

- [x] Filled in all system information
- [x] Included actual terminal outputs (not just screenshots)
- [x] Provided at least 2 screenshots (Python tests + ROS talker/listener)
- [x] Documented 2–3 real problems with solutions
- [x] Completed the AI usage section with exact prompts
- [x] Written a thoughtful reflection (3–5 sentences)
- [x] Signed the declaration

---

**End of Report**

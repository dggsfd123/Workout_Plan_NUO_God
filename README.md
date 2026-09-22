# 诺神的健身打卡 Workout Plan of NUO God

一个简单的本地优先健身打卡网页。读一个 `plan.json` 训练计划，每天按顺序打卡，划掉一条自动显示下一条，全部完成显示「今日训练结束」；休息日显示「今日休息」。纯静态、零依赖，可直接用 GitHub Pages 免费分发。

## 功能特性

- 读本地 `plan.json`，按「第几天」展示训练计划
- 每组一条任务（动作 / 重量 / 次数 / 第几组 / 组间休息），点一下划掉并跳到下一条
- 休息日支持「纯休息」与「休息 + 有氧」两种
- 自动跳到今天（或下一个未完成）的训练日；纯休息日自动跳过
- 底部统计本轮已完成组数（只统计动作，不含拉伸）
- 顶部个人信息（年龄 / 身高 / 体重 / BMI / 目标），BMI 自动计算
- 网页内可弹窗编辑动作、可把改动保存回 `plan.json`
- 进度按日期存本地，刷新不丢

## 给自己用（每周更新计划）

每周只需在本地改 `plan.json`，然后推到**你自己新建的仓库**即可，无需改动任何代码。

1. 克隆 / 下载本仓库到本地
2. 编辑 `plan.json`（格式见下方），写上你这一周的计划
3. 在 GitHub 新建一个**私有或公有**仓库（可只给自己看）
4. 把本仓库文件上传进去：
   ```cmd
   git init
   git add plan.json index.html README.md
   git commit -m "我的训练计划"
   git branch -M main
   git remote add origin https://github.com/<你的用户名>/<你的仓库名>.git
   git push -u origin main
   ```
5. 开启分发：仓库 **Settings → Pages → Source** 选 `Deploy from a branch` / `main` / `/(root)` → Save
6. 等一两分钟，访问 `https://<你的用户名>.github.io/<你的仓库名>/` 就是你的在线打卡页，手机也能直接打开

之后每周改完 `plan.json`，重复：
```cmd
git add plan.json
git commit -m "更新本周计划"
git push
```
GitHub Pages 会自动更新，无需其他操作。

## plan.json 格式

- `profile`：个人信息，可选；`height` / `weight` 可带单位（如 `186cm`），BMI 自动按数值计算；`goal` 取 `增肌` / `减脂` / `增肌&减脂`
- `days[].date`：日期，格式 `YYYY-MM-DD`
- `days[].type`：`training`（训练日）或 `rest`（休息日）
- `days[].exercises`：
  - 每个动作含 `name` / `weight` / `reps` / `sets` / `rest`
  - 任意字段缺失或写 `-` 都表示「无」，界面以 `—` 显示
  - `rest` 日**没有任何 `exercises`** 时显示「今日休息」；**有 `exercises`**（如轻松有氧）则照常列出打卡
- 一个动作的 `sets` 会被展开成「每组一条」任务（如 4 组 = 4 条）

> 网页内改的动作 / 个人信息只存在浏览器本地（叠加层），不覆盖文件；点「保存计划到文件」可把合并结果下载回 `plan.json` 提交。若想完全以文件为准，点「清除本地修改」。

## 引用本项目

本模板开源供自行使用与二次分发。若你基于它搭建并分享给他人，请保留对本项目的引用：

- 项目地址：https://github.com/dggsfd123/Workout_Plan_NUO_God
- 引用方式（在转发时注明来源即可）：「基于 Workout_Plan_NUO_God 健身打卡模板搭建」

---

纯静态、零后端，数据全在你自己的 `plan.json` 与浏览器本地，隐私可控。

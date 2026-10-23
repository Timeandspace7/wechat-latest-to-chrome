---
name: wechat-latest-to-chrome
description: Find the newest non-pinned article in a specified WeChat Official Account, open it in the user's default Chrome browser, scroll to the bottom, and read the article with image inspection and a concise summary.
---

# WeChat latest article to Chrome

Use this skill when the user asks to move the newest article from a named WeChat Official Account into Chrome. The account name is an input; examples such as “小黑黑小小” or “饕餮海投资” are not defaults.

## Workflow

1. Bring the WeChat window to the foreground. Inspect the current WeChat window and re-observe after every navigation or scroll. Act on the current accessibility tree or screenshot; never rely on fixed coordinates, stale element indexes, or a remembered window state.
2. Open the Official Accounts area and search for or select the requested account. Confirm the account name in the account/profile page before selecting an article. If multiple accounts have similar names, stop and report the ambiguity.
3. Open the account's article list and identify the newest dated article. Treat blocks labeled “置顶” as pinned and exclude them from recency selection. Compare the visible publication dates using the newest actual date/time; do not infer recency from card order alone. Record the account name, title, date/time, and canonical article link if available.
4. Open the selected article and verify its header still matches the account, title, and date recorded in step 3. If it does not, return to the list and re-evaluate.
5. From the article's current menu, choose “用默认浏览器打开” when present. Wait for the browser window to appear and verify its title or visible page heading matches the selected article. If that menu item is unavailable or fails, use “复制链接”, then paste the copied URL into the already-open Chrome address bar; do not use a guessed or reconstructed URL.
6. After the target article is loaded in Chrome, send the End key to the verified Chrome window to move the article to the bottom. Use a fresh window handle from the current app inventory; do not assume the previous Chrome window or tab is still active.
7. Read and organize the article. Prefer the configured WeChat article-reading MCP for the canonical https://mp.weixin.qq.com/s/... URL when browser DOM access is unavailable. Record the title, account, publication time, body text, image count, and video count. Inspect each returned image for its role and salient information, then produce a concise Chinese summary. Clearly separate facts stated in the article from the author's opinions, holdings, forecasts, and disclaimers.
8. Report the verified account, article title, publication date, Chrome result, bottom-scroll action, image check, and concise summary. If a step cannot be verified, stop at that step and state the exact reason. Do not perform extra confirmation or exploratory steps beyond this workflow.

## Boundaries and failure handling

- Do not clip, publish, or edit the article. This rollback only covers opening, bottom scrolling, reading, image inspection, and summarization.
- Do not bypass login, CAPTCHA, remote-debugging approval, or site-safety restrictions. If WeChat is logged out, a CAPTCHA appears, or the UI cannot be safely identified, stop and report it.
- A successful run requires metadata verification in WeChat, a Chrome window/page whose title or heading matches the selected article, an End key action, and a reported reading result.
- If no article newer than the last recorded link exists, report that no new article was found and do not open a pinned duplicate.

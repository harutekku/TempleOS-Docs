# Windows

Only tasks on Core0 can have a window and there can be only one window per task. The window Z-buffer, top-to-bottom order is determined by the order in the task queue, with the WinMgr on the bottom. A task can have child task popup windows.

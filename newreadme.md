## PAttn
1.type "bash ./script/ETTh.sh" since folder name is script instead of scripts

2.Issue:
AttributeError: `np.Inf` was removed in the NumPy 2.0 release. Use `np.inf` instead.  
This is a known breaking change introduced in NumPy 2.0.  

✅ Fix: Modify tools.py  
Edit the file:

LLMsForTimeSeries/PAttn/utils/tools.py  
Find line 50 (or nearby):

self.val_loss_min = np.Inf  
Replace it with:  

self.val_loss_min = np.inf  
🔁 Repeat this for any other occurrences of np.Inf.  

✅ Why This Works:  
In NumPy < 2.0, both np.Inf and np.inf were allowed.  

In NumPy 2.0, np.Inf was removed for consistency — use lowercase np.inf.

3.FileNotFoundError: [Errno 2] No such file or directory: './datasets/ETT-small/ETTh1.csv'  
Because the script you're running likely uses:  

--root_path ./datasets/ETT-small/  
instead of:  

--root_path ../datasets/ETT-small/  
That makes the script look for:  

bash  

./datasets/ETT-small/ETTh1.csv  
which does not exist inside PAttn/.  

✅ Fix It Now  
✏️ Edit script/ETTh.sh  
Find this line (or similar):  

--root_path ./datasets/ETT-small/  
Change it to:  

--root_path ../datasets/ETT-small/  
Do this for both ETTh1 and ETTh2 blocks inside ETTh.sh.  

✅ Then re-run:  

bash ./script/ETTh.sh  
That should finally solve the FileNotFoundError. Let me know if you want me to regenerate the fixed version of ETTh.sh for you.  

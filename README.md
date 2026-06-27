# generate_100_commits.py
import os
import subprocess
from datetime import datetime

def run_command(cmd):
    subprocess.run(cmd, shell=True, check=True)

# Configuration
repo_path = "."          # Run this INSIDE your cloned public repo
commits_needed = 100     # ← Changed to 100

os.chdir(repo_path)

print(f"🚀 Starting {commits_needed} public commits...")

for i in range(1, commits_needed + 1):
    filename = f"contribution_{i:03d}.py"
    
    content = f'''# contribution_{i:03d}.py
# Public commit #{i} - Active Open Source Contributor

def milestone_message():
    return "This is public commit #{i} toward the 100 commit goal! 🔥"

def get_stats(n={i}):
    """Demo function for contribution tracking"""
    return {{
        "commit_number": n,
        "status": "public",
        "timestamp": "{datetime.now().isoformat()}",
        "progress": f"{{n}}/{{commits_needed}} completed"
    }}

if __name__ == "__main__":
    print(milestone_message())
    stats = get_stats()
    print(f"Commit: {{stats['commit_number']}} | Status: {{stats['status']}}")
'''

    # Write the file
    with open(filename, "w") as f:
        f.write(content)
    
    # Commit
    run_command(f"git add {filename}")
    run_command(f'git commit -m "feat: add contribution #{i:03d}\\n\\n- Created contribution_{i:03d}.py\\n- Progress toward 100 public commits milestone\\n- Auto-generated open source contribution"')
    
    print(f"✅ Commit {i}/{commits_needed} completed")

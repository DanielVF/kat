# kat
Shortcut to launch Claude code in a new directory from a fish shell

```
function katnew --description "Create a new dated project directory and open in Claude Code"
    # Validate argument
    if test (count $argv) -eq 0
        echo "Usage: katnew <project-name>"
        return 1
    end

    # Build directory path with today's date
    set -l date_prefix (date +%Y-%m-%d)
    set -l project_name $argv[1]
    set -l project_dir ~/projects/$date_prefix-$project_name

    # Create project directory and .claude config directory
    mkdir -p $project_dir/.claude

    # Create settings.json with acceptEdits mode (trusts edits, keeps other safety checks)
    echo '{"permissions": {"defaultMode": "acceptEdits"}}' > $project_dir/.claude/settings.json

    # Enter directory and launch Claude
    cd $project_dir
    ~/.local/bin/claude
end
function kat
    ~/.local/bin/claude
end
```

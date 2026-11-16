# Calisthenics Quest

A static 12-week workout tracker. It retains the existing progression, day-specific workouts, sets and reps, weekly check-offs, habits, notes, optional weight logs, and visual styling. Tracker data is saved in browser localStorage and is not included in the repository.

## Protect existing Edge progress

Before replacing or moving your old tracker, open it in Edge and export its localStorage. In the old tracker, press F12, open Console, and run:

```js
const backup = { origin: location.origin, exportedAt: new Date().toISOString(), localStorage: Object.fromEntries(Array.from({length: localStorage.length}, (_, i) => { const key = localStorage.key(i); return [key, localStorage.getItem(key)]; })) };
const link = document.createElement("a");
link.href = URL.createObjectURL(new Blob([JSON.stringify(backup, null, 2)], {type: "application/json"}));
link.download = "calisthenics-quest-edge-backup.json";
link.click();
URL.revokeObjectURL(link.href);
```

Keep that JSON somewhere safe. Then open the upgraded tracker in Edge, choose **Import backup**, review its preview, and select **Merge** or **Replace**. Keep both backups until you verify the restored progress. Browser profiles and origins (old file, local file, Pages URL) keep separate localStorage. Never clear Edge site data or delete the old tracker until migration is verified.

## Backup behavior

- Export produces a versioned JSON backup.
- Import validates format, version, fields, week/day keys, and limits before preview; invalid files do not change data. It also accepts the Edge localStorage export above.
- Merge combines check-offs and lets the imported backup win for overlapping notes, weights, habits, and completion flags. Replace confirms first and downloads a backup of current data.
- The original `calisthenicsQuestV1` storage key is preserved. Storage errors appear in the app; unsafe automatic writes pause if saved data cannot be read.
- Backups can contain private notes and body-weight records. Do not commit JSON backups.

## Run locally

Open `index.html` in Edge or another modern browser. Each browser origin has separate storage; import your Edge backup into the copy you will use.

## GitHub repository

The project files (`index.html`, `README.md`, `.gitignore`) are uploaded to the private repository [venkateswaran0509/personal-development](https://github.com/venkateswaran0509/personal-development), on `main`. Commit `958a53f` added the tracker. No personal backup JSON was uploaded. The repository remains private; GitHub Pages is not enabled.

## GitHub Pages

Pages access depends on plan and repository settings. A private source repository does not make a Pages website private: Pages sites are public by default. Private Pages access control requires an organization using GitHub Enterprise Cloud. Publishing may expose the app source; personal tracker data remains in each browser and is not included in the files. To enable Pages, use **Repository Settings > Pages**, select **Deploy from a branch**, choose `main` and `/(root)`, then save. Review visibility before sharing. See [GitHub Pages plan availability](https://docs.github.com/en/pages/getting-started-with-github-pages), [private Pages sites](https://docs.github.com/en/enterprise-cloud%40latest/pages/getting-started-with-github-pages/about-privately-published-github-pages-sites), and [changing Pages visibility](https://docs.github.com/en/enterprise-cloud%40latest/pages/getting-started-with-github-pages/changing-the-visibility-of-your-github-pages-site).

## Exercise references

The source includes text cues but no exercise image files or image references; the available cues and layout are retained.

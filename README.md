# Calisthenics Quest

A single-file, static 12-week workout tracker. Workout data stays in the browser's local storage; it is not uploaded to GitHub. The existing workout progression, day-specific logic, weekly check-offs, daily habits, notes, optional weekly weight entry, and visual styling are retained.

## Protect and migrate your Edge progress first

Do this **before replacing, moving, or renaming the old tracker**:

1. In Microsoft Edge, open the old working tracker from its existing location. Do not clear Edge site data or delete the old file.
2. Press **F12**, open **Console**, and run the snippet below. If Edge asks you to allow pasting, follow its displayed safety prompt. It downloads the current page's local storage as JSON.
3. Keep the downloaded `calisthenics-quest-edge-backup.json` in a safe place. The file may contain personal workout notes and weight entries.
4. Open the upgraded tracker in the same browser and use **Import backup**. Review the backup preview and choose **Merge** or **Replace**. Merge combines check-offs and keeps both browsers' entries; where notes, weights, habits, or completion flags overlap, the imported backup takes precedence. Replace downloads a pre-restore backup before applying the imported data.
5. Confirm the imported weeks, notes, and weight entry in the tracker. Keep both backup files until you have confirmed the migration.

```js
const backup = {
  origin: location.origin,
  exportedAt: new Date().toISOString(),
  localStorage: Object.fromEntries(
    Array.from({ length: localStorage.length }, (_, i) => {
      const key = localStorage.key(i);
      return [key, localStorage.getItem(key)];
    })
  )
};
const link = document.createElement("a");
link.href = URL.createObjectURL(
  new Blob([JSON.stringify(backup, null, 2)], { type: "application/json" })
);
link.download = "calisthenics-quest-edge-backup.json";
link.click();
URL.revokeObjectURL(link.href);
```

Browser local storage is separated by browser profile and site origin. The old `file://` copy, a local development server, and a GitHub Pages URL may each have separate storage. Use JSON export/import to move data between them.

## Backups and data safety

- **Export backup** saves a versioned JSON file containing all tracker data. Export periodically and before browser changes.
- **Import backup** validates the format, version, field types, week/day keys, and data limits before showing a preview. Invalid files do not change tracker data.
- **Merge** keeps existing and imported check-offs; the imported backup wins for matching notes, weights, habits, and session completion values.
- **Replace** asks for a separate confirmation and downloads the current data first.
- Local storage errors are shown in the page. If saved data cannot be read, automatic writes are paused to avoid silently replacing it.
- Keep JSON backups private. They can contain notes and body-weight records. Do not commit them to GitHub.

The import supports both this app's versioned backup and the Edge local-storage export snippet above. The app preserves the original local-storage key (`calisthenicsQuestV1`) so an upgraded copy opened at the same origin can continue using existing saved data.

## Run locally

Open `index.html` in a current browser. For local development, a simple static server also works. Each origin has its own local storage, so import the Edge backup into whichever browser/origin you will use.

## Prepare a private GitHub repository

1. The private repository has been created: [venkateswaran0509/personal-development](https://github.com/venkateswaran0509/personal-development). GitHub converts the requested space to a hyphen in the repository URL.
2. Add `index.html`, `README.md`, and `.gitignore`. Do not add personal JSON backups.
3. Commit and push only after reviewing the files and confirming the Edge backup is safely stored. The repository is currently empty; these project files and your workout data have not been uploaded, committed, or published.

### GitHub Pages visibility

GitHub Pages availability depends on the plan: GitHub Free supports Pages for public repositories; paid plans such as Pro support Pages from private repositories. A private source repository does **not** automatically make the website private. Pages sites are public by default, including sites built from private repositories, unless the organization has the Enterprise Cloud private-site access feature and configures it. Personal workout data remains in browser local storage and is not included in the published files, but anyone with access to a public site can use their own browser copy.

To publish, after the reviewed files are pushed, open **Repository → Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, select the intended branch (usually `main`) and `/(root)`, then save. Review the site's visibility setting before sharing its URL. Publishing a public site may expose the app source even while the repository remains private. For private site access control, GitHub's documentation currently requires an organization on GitHub Enterprise Cloud. See [GitHub Pages plan availability](https://docs.github.com/en/pages/getting-started-with-github-pages), [private Pages sites](https://docs.github.com/en/enterprise-cloud%40latest/pages/getting-started-with-github-pages/about-privately-published-github-pages-sites), and [changing Pages visibility](https://docs.github.com/en/enterprise-cloud%40latest/pages/getting-started-with-github-pages/changing-the-visibility-of-your-github-pages-site).

## Existing exercise references

The located tracker file contains text form cues for each exercise but no exercise image files or image references. This copy keeps the available cues and layout intact; it does not invent or substitute illustrations.

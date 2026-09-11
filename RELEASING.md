# First release and citation metadata

The repository has no release tag or Zenodo DOI yet. `CITATION.cff` and
`.zenodo.json` describe the project without claiming a released version or date.

## Prepare the first release

1. Select the exact repository revision and database snapshot used for the
   manuscript. Record the full commit SHA and the included data sources in the
   release notes; the current default branch need not match the analysis used.
2. Choose the first release version and publication date. Add `version` and
   `date-released` (`YYYY-MM-DD`) to `CITATION.cff`, and matching `version` and
   `publication_date` strings to `.zenodo.json`. If the Git tag has a `v` prefix,
   use the same version without that prefix in both metadata files.
3. Review the author order, names, ORCIDs, affiliations, title, description,
   keywords, and license together. Keep both files in UTF-8 without a byte-order
   mark. Affiliations are included only where known.
4. Validate the metadata before merging the release preparation:

   ```sh
   python -m venv .venv-citation
   .venv-citation/bin/python -m pip install cffconvert
   .venv-citation/bin/cffconvert --validate
   .venv-citation/bin/python -m json.tool .zenodo.json
   git diff --check
   ```

   On Windows, use `.venv-citation/Scripts/python.exe` and
   `.venv-citation/Scripts/cffconvert.exe` instead of the corresponding `bin`
   paths. Keep the temporary environment out of Git, for example with a local
   `.git/info/exclude` entry. Validation checks file structure; review matching
   creator names, order, affiliations and ORCIDs in both files as well.

## Publish and archive (manual maintainer actions)

1. Enable this repository in the maintainer's
   [Zenodo GitHub integration](https://help.zenodo.org/docs/github/).
2. After merging the reviewed release metadata, create the selected Git tag on
   the intended revision and publish a GitHub release. Include the analysis
   provenance and database snapshot details in the release notes.
3. Follow Zenodo's [archive-a-release guide](https://help.zenodo.org/docs/github/archive-software/github-upload/)
   and verify that processing succeeded and the record contains the intended
   revision and metadata.
4. Copy the actual version-specific DOI into `CITATION.cff` as `doi` and update
   the README citation section with that DOI and the DOI badge supplied by
   Zenodo. A concept DOI can link readers to all versions; use the version DOI
   when citing the exact snapshot in the manuscript. Do not invent a DOI or
   retag the archived release to include this subsequent metadata update.

When both metadata files exist,
[Zenodo uses `.zenodo.json` for archiving](https://help.zenodo.org/docs/github/describe-software/zenodo-json/),
so updates to `CITATION.cff` alone do not update archive metadata. Keep their
shared fields synchronized. Do not copy a previous release's DOI into a new
release's `.zenodo.json`; let the integration assign the new archive's DOI.

For every later release, update both version and date fields before tagging,
revalidate the files, and verify the resulting Zenodo record. Refresh the
version-specific DOI in the citation metadata and README after archiving.

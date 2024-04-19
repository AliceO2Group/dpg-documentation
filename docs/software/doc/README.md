# Software releases for asynchronus reconstruction and simulation

```warning
The names of branches and tags used throughout this page are drafts and subject to change.
```

```note
From now on, requests have to be made by labelling the corresponding PRs with the respective labels.
Opening additional MRs in this repository is obsolete.
For dedicated information, please see [below](#mark-prs-to-be-cherry-picked-with-labels).
```

## Branch, cherry-pick, tag, release

O2 and related software evolves over time. The global evolvement/development happens on their corresponding default branches.

Whenever data is reconstructed, that is done with a certain state of the software at that point in time. In that sense, one could say that running a new reconstruction campaign effectively **tags** the software.
In our case, the actual act of **tagging** happens on the level of `git`s history of our software packages.
Hence, whenever a new reconstruction campaign is run on data, the default branches shall be tagged at their current stage and a new branch, specifically for that reconstruction pass, is created from that tag. Any further reconstruction or simulation related to that reconstruction campaign is done based on that branch.

The figure below sketches the workflow branching, tagging and release procedure.

While still all developments go into the default branches, some of them might be necessary bug fixes or some required features that should for instance be used in upcoming simulation productions.
Those specific developments find their way into the branch of a given reconstruction pass via cherry-picking the corresponding commits from the default branch.
All new software releases for a given reconstruction pass correspond to tags derived from the branch of the reconstruction pass.

Packages affected by the approach are:

* O2,
* O2DPG,
* O2Physics,
* QualityControl (decision not yet final, to be discussed with the developers).

Packages that will be tagged in the same way (for consistency and transparency) but where no cherry-picks or dedicated PRs from user are taken:

* alidist.

![RelVal general](../../files/images/software_branching_tagging_overview.png)

## Mark PRs to be cherry-picked with labels

Whenever a bug fix or required feature needs to be contained in certain branch, the PR with those development must be annotated with the label that corresponds to the branch of the desired reconstruction campaign.
Adding such a label means to **request** that this PR should be ported into the release branches to end up in the next software tag.

```note
Labels can be added anytime but only PRs that have been **merged** into the default branches can be ported.
```

If the author of a PR has the possibility, labels can be added directly to a PR. However, if the role of the author does not allow to add labels, a comment can be issued in the PR that will trigger adding the labels.
As of now, whenever a PR is (re)opened (so far functional in O2 and O2DPG), there will be an automatic message at as the first comment to that PR:

```instruction
**REQUEST FOR PRODUCTION RELEASES:**
To request your PR to be included in production software, please add the corresponding labels called "async-<name>" to your PR. Add the labels directly (if you have the permissions) or add a comment of the form (note that labels are separated by a ",")

`+async-label <label1>, <label2>, !<label3> ...`

This will add `<label1>` and `<label2>` and removes `<label3>`.

**The following labels are available**
async-2022-pp-apass4
async-2023-pbpb-apass3
async-2023-pp-apass4
async-2022-pp-apass6-2023-PbPb-apass2
```

Each label corresponds to a page where the **approved** requests are listed. The mapping of labels and pages is the following:

* [async-2022-pp-apass4](../requests/2022pp_apass4.md),
* [async-2023-pbpb-apass3](../requests/2023pbpb_apass3.md),
* [async-2023-pp-apass4](../requests/2023pp_apass4.md),
* [async-2022-pp-apass6-2023-PbPb-apass2](../requests/2022pp_apass6.md).

## Reviewing and accepting PRs

A list of collected PRs for upcoming software releases shall be presented during the weekly WP12/13 meeting, Wednesdays at 15:00 CERN time. That requires requestors to be present in the meeting in case there are questions or doubts concerning their PRs.

```warning
Only requests that have been made before Wednesday 12:00 CERN time can be considered.
Requested PRs must be **merged** by that point, otherwise they cannot be considered.
PRs that were not accepted during the meeting will not be added to the release branches.
```

All accepted PRs will then be ported to the release branches and the tags will be prepared before the weekend.
It is possible for the DPG to decide to not release tags when only minor changes are requested. That means that new tags are released at most once a week.
Once ported, the PR will be marked by the operator with a `<reuqested-label>-acc` label.

## Patching a tag

While tags are derived from the release branches, already existing tags can be patched. That is however only done if absolutely necessary. The convention is to add a letter at the end of the original tag name. For instance, the third patch of tag `v1-2-3` will be named `v1-2-3c`.
If patching a tag is requested, the corresponding PRs shall not only be cherry-picked on top of the tag but they shall also go into the release branch such that all following regular tags will contain the patch as well. Once a patched tag has been released, the previous ones become obsolete and shall not be used anymore for any reconstruction or simulation. Following the example above, tags `v1-2-3`, `v1-2-3a` and `v1-2-3b` will be obsolete as soon as `v1-2-3c` has been released. All those patches will be contained in the branch `v1-2`.

```note
If a patch is requested but the next tag does not yet exist, there will be no patched tag but the next one will be created directly. For instance, if a patch if requested for tag `v1-2-3` but the tag `v1-2-4` does not yet exist, it will be created. Tag `v1-2-3` shall be marked as obsolete.
```

```warning
Patched tags will have no immediate correspondence to a branch in terms of commit history/hashes.
```

### Collect the PRs/commits for a tag

Here, let's take the O2DPG repository as an example.

One can go to the [closed PRs](https://github.com/AliceO2Group/O2DPG/pulls?q=is%3Apr+is%3Aclosed+label%3Aasync-2022-pp-apass4) for the `async-2022-pp-apass4` label to see all closed PRs containing that label.
At any time, one can filter by any other label.
In addition, to filter by "when a PR was merged", [this URL](https://github.com/AliceO2Group/O2DPG/pulls?q=is%3Apr+is%3Aclosed+merged%3A2023-03-19..2024-03-19+label%3Aasync-2022-pp-apass4) can be used as a starting point.
It filters the PRs taking into account given labels and the time interval in which PRs were merged.

{% include list.liquid all=true %}

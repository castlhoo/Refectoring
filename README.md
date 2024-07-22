# Refectoring

## TalentDonationProjectService.java
1. getDonationProject(String projectName):
``` public TalentDonationProject getDonationProject(String projectName) {
    return donationProjectList.stream()
            .filter(project -> project != null && project.getTalentDonationProjectName().equals(projectName))
            .findFirst()
            .orElse(null);
}

```
2. donationProjectUpdate(String projectName, Donator people):

```
public void donationProjectUpdate(String projectName, Donator people) throws Exception {
    TalentDonationProject project = donationProjectList.stream()
            .filter(p -> p != null && p.getTalentDonationProjectName().equals(projectName))
            .findFirst()
            .orElseThrow(() -> new Exception("프로젝트 이름과 기부자 정보 재 확인 하세요"));

    if (people != null) {
        project.setProjectDonator(people);
    } else {
        throw new Exception("프로젝트 이름은 있으나 기부자 정보 누락 재확인 하세요");
    }
}
```

3. beneficiaryProjectUpdate(String projectName, Beneficiary people):
```
public void beneficiaryProjectUpdate(String projectName, Beneficiary people) throws Exception {
    TalentDonationProject project = donationProjectList.stream()
            .filter(p -> p != null && p.getTalentDonationProjectName().equals(projectName))
            .findFirst()
            .orElseThrow(() -> new Exception("프로젝트 이름과 기부자 정보 재 확인 하세요"));

    if (project != null) {
        project.setProjectBeneficiary(people);
    } else {
        throw new Exception("프로젝트 이름은 있으나 기부자 정보 누락 재확인 하세요");
    }
}
```

## EndView.java
1. projectView(TalentDonationProject project):
```
public static void projectView(TalentDonationProject project){
    Optional<TalentDonationProject> pr = Optional.ofNullable(project);
    pr.ifPresentOrElse(
            pro -> System.out.println(pro),
            ()-> System.out.println("해당 프로젝트가 존재하지 않습니다.(수정)")
    );
}
```
2. projectListView(ArrayList<TalentDonationProject> allProbonoProject):
```
public static void projectListView(ArrayList<TalentDonationProject> allProbonoProject){
    AtomicInteger index = new AtomicInteger(1);
    allProbonoProject.forEach(project -> {
        if (project != null) {
            System.out.println("[진행 중인 project : " + index.getAndIncrement() + "] " + project);
        }
    });
}
```

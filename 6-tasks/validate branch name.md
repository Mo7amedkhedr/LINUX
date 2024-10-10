
# validate branch name


```

#include <iostream>
#include <regex>
#include <string>

bool validateBranchName(const std::string& branchName) {
    // Regex pattern
    std::regex pattern(R"(^feature\/[A-Z]{2}-\d{3}\/[a-zA-Z0-9-_]+$)");
    return std::regex_match(branchName, pattern);
}

int main() {
    std::string branchName = "feature/TN-123/branchname";

    if (validateBranchName(branchName)) {
        std::cout << "Valid branch name" << std::endl;
    } else {
        std::cout << "Invalid branch name" << std::endl;
    }

    return 0;
}
```

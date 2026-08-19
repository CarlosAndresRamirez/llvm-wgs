# **Wednesday, July 22, 9:00 \- 10:00 am CDT**

# **Agenda**

7. Prior minutes are now in https://github.com/llvm/llvm-wgs/tree/main/offload-wg/meeting-minutes  
8. PR Review list  
   1. Add nodiscard support to offload-tblgen and mark olInit  
      1. https://github.com/llvm/llvm-project/pull/209727  
      2. See if \[\[nodiscard\]\] can be applied to a type in C23  
   2. Split olMemAlloc to separate functions  
      1. https://github.com/llvm/llvm-project/pull/209196  
      2. Removes “device” parameter for host allocations  
      3. Joseph: splitting host allocations makes sense, the other two could be decided by flags  
   3. Review request \+ offload context update  
      1. [https://github.com/llvm/llvm-project/pull/209144](https://github.com/llvm/llvm-project/pull/209144)  
   4. https://github.com/llvm/llvm-project/pull/210737  
      1. Alex: for direct linking the presence of symbols could be checked at configuring time  
      2. Direct linking used to be the only option, but it forced having all libraries present at compilation time.  
      3. Could dlopen/dlsym be used with direct linking?  
         1. There are still similar issues as those addressed by weak symbols  
         2. Example of a prior approach to a similar issue: https://github.com/llvm/llvm-project/blob/main/flang-rt/lib/runtime/io-api-server.cpp\#L301  
9. SYCL offload context discussion  
   1. https://github.com/llvm/llvm-project/pull/201398    
   2. Joseph: generally ok, some things were already intended to be handled by plugins  
   3. Lukasz: there are additional trackers needed, for example to track shared memory allocations for the AMDGPU plugin  
   4. Joseph: it’s strange that there is still a global state even with the context present  
   5. Lukasz: the PR is still not a final implementation, more cleanup can be done  
   6. Lukasz: the context is needed for SYCL and OpenCL, not specifically for L0  
   7. Cleanup ongoing, resolving merge conflicts  
   8. Added additional APIs with mem alignment  
   9. The API changes are split in several PRs  
      1. Initial one is ‘c’ on the PR review list  
10. OpenACC support  
    1. https://github.com/llvm/llvm-project/pull/213784  
       (https://github.com/llvm/llvm-project/pull/208113 will be rebased on top of above)  
    2. \[Prior discussion in meeting minutes...\]  
    3. Compiler support (in flang) will be upstreamed in parallel.  
    4. Ivan will start creating non-draft PRs  
    5. PRs:  
       https://github.com/llvm/llvm-project/pull/208113  
       https://github.com/llvm/llvm-project/pull/208205  
    6. These two PRs are preparing the runtime to split the common parts for OpenMP and OpenACC.  Will use a linker script to export only the relevant names, based on the way that GCC/Clang mangle symbols.  
    7. Will still need to do this with MSVC  
    8. The common library will export both OpenMP and OpenACC functions  
    9. Joseph: this is only necessary if someone uses both at the same time. Otherwise two separate shared libraries would suffice  
    10. Joseph: Having OpenMP and OpenACC share mappings, for example, would be difficult to implement, possibly with unexpected consequences for the user.  
    11. Ivan: Johannes wanted both to cooperate.  
    12. Ivan: can implement the separate libraries first and revisit the cooperative case later.  
    13. Once the two PRs are merged, Ivan will create a PR that splits the common parts into a separate library.  
    14.   
11. RFC “Proposed extension to the \--offload-arch option”.  What are the remaining open issues, and how can we drive this to a conclusion?  
    1. RFC: https://discourse.llvm.org/t/rfc-proposed-extension-to-the-offload-arch-option/90790  
    2. Joseph: concerned about increase in complexity in the driver, these flags should instead be toolchain-specific; not opposed to the options existing  
    3. Greg: specifying virtual ISAs is common enough to warrant a driver (top-level) option, rest can be toolchain-specific.  
    4. Joseph: ok with that. More discussion (about specific option naming/syntax) to follow  
    5. The discussion will continue in PRs.  
    6. Aaron Ballman asked in the RFC thread about the status of it.  The RFC was approved with the rest of the discussion deferred to PRs.  
12. Lukasz still waiting for the offload-reviewers team.  
    1. There is 3 people that can accept me to the team:  
       1. ![][image1]

13. Lukasz: No testing of offload in pre-commit PRs.  
    1. Joseph: we should have building of offload libraries as a part of the pre-commit CI  
    2. Joseph: Running tests is disabled because some of them are expensive, plus there are lots of flaky tests.  
    3. Lukasz: it would be nice to be able to test offload via common CI  
14. Lukasz: are we active on discord?  
    1. Channels: runtime or openmp.

15. Lukasz is still waiting for the offload-reviewers team.  
    1. There is 3 people that can accept me to the team

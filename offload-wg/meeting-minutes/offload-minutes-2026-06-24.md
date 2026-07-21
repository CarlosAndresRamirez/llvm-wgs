# **Wednesday, June 24, 9:00 \- 10:00 am CDT**

# **Agenda**

11. Prior minutes are now in [https://github.com/llvm/llvm-wgs/tree/main/offload-wg/meeting-minutes](https://github.com/llvm/llvm-wgs/tree/main/offload-wg/meeting-minutes)  
12. PR Review list  
13. SYCL offload context discussion
    1. [Slides](slides/offload-context-2026-06-24.org)
    2. [https://github.com/llvm/llvm-project/pull/201398](https://github.com/llvm/llvm-project/pull/201398)     
    3. Joseph: generally ok, some things were already intended to be handled by plugins  
    4. Lukasz: there are additional trackers needed, for example to track shared memory allocations for the AMDGPU plugin  
    5. Joseph: it’s strange that there is still a global state even with the context present  
    6. Lukasz: the PR is still not a final implementation, more cleanup can be done  
    7. Lukasz: the context is needed for SYCL and OpenCL, not specifically for L0  
14. Follow up proposal to OL\_KERNEL\_LAUNCH\_PROP\_TYPE\_SIZE:   [https://github.com/llvm/llvm-project/pull/194333](https://github.com/llvm/llvm-project/pull/194333) (merged)  
    1. Piotr working on a follow-up  
    2. [https://github.com/llvm/llvm-project/pull/205224](https://github.com/llvm/llvm-project/pull/205224)  
    3. Accepted, can be merged now  
15. Host plugin seems to run each function once, unlike GPU plugins that execute the kernels multiple times.  
    1. Joseph: the host plugin historically has been intended to test the OpenMP implementation, without attempts to optimize it; it can be improved  
    2. Piotr: SYCL has a “native” CPU support.  Unifying the plugin structure would be helpful   
    3. Joseph: it would be good to get the offload test suite to pass with the host plugin  
16. Windows support for SYCL  
    1. PR: [https://github.com/llvm/llvm-project/pull/187006](https://github.com/llvm/llvm-project/pull/187006) (merged)  
       1. [Compiling liboffload on Windows](https://github.com/llvm/llvm-project/pull/187006)  
       2. [L0 implementation still needs a few tweaks](https://github.com/llvm/llvm-project/pull/187006)  
       3. [It now works with Windows.  PR to be updated this week.](https://github.com/llvm/llvm-project/pull/187006)  
    2. Joseph: the bulk of this is generic C code, so it shouldn’t be hard to get it working  
    3. All comments in the main PR have been addressed.  
    4. There is one additional PR related to this: [https://github.com/llvm/llvm-project/pull/202540](https://github.com/llvm/llvm-project/pull/202540) (merged)  
    5. Unit tests still to come  
17. OpenACC support  
    1. NVIDIA is in the process of upstreaming OpenACC support in flang.  Will also upstream runtime implementation.  
    2. Has prototype that uses liboffload/libomptarget  
    3. RFC will published soon (within a couple of weeks)  
    4. Joseph: sounds reasonable  
       1. Noted that libomptarget should depend on liboffload, not the other way around.  
       2. Public buildbot would be good to have  
    5. Still working on it.  Making sure that the code that was going to be published with the RFC is in a good shape.  
    6. RFC: [https://discourse.llvm.org/t/openacc-runtime-in-llvm-offload-libacctarget/90793](https://discourse.llvm.org/t/openacc-runtime-in-llvm-offload-libacctarget/90793)  
    7. PR: https://github.com/llvm/llvm-project/pull/197894  
    8. The dependence issue may be addressed later.  Common code may be extracted into a support library.  
    9. There will need to be a buildbot to test the OpenACC code.  
       1. Joseph: we should have unit tests that will have better coverage (than OpenMP tests) including corner cases.  
    10. Compiler support (in flang) will be upstreamed in parallel.  
    11. Ivan will start creating non-draft PRs  
18. RFC [“Proposed extension to the \--offload-arch option”](https://discourse.llvm.org/t/rfc-proposed-extension-to-the-offload-arch-option/90790).  What are the remaining open issues, and how can we drive this to a conclusion?  
    1. RFC: [https://discourse.llvm.org/t/rfc-proposed-extension-to-the-offload-arch-option/90790](https://discourse.llvm.org/t/rfc-proposed-extension-to-the-offload-arch-option/90790/23)  
    2. Joseph: concerned about increase in complexity in the driver, these flags should instead be toolchain-specific; not opposed to the options existing  
    3. Greg: specifying virtual ISAs is common enough to warrant a driver (top-level) option, rest can be toolchain-specific.  
    4. Joseph: ok with that  
    5. More discussion (about specific option naming/syntax) to follow



Websites can vary in how strictly they match the path of an incoming request to a defined endpoint. For example, they may tolerate inconsistent capitalization, so a request `/ADMIN/DELETEUSER` will still be mapped to `/admin/deleteuser` endpoint. Otherwise, it may treat these as two different endpoints and fail to enforce the correct restrictions as a result.

Similar discrepancies can arise if the `useSuffixPatternMatch` option in Sprint framework is enabled, as this allows paths with an arbitrary file extension to be mapped to an equivalent endpoint with no file extension. For example, a request to `/admin/deleteUser.anything` would still match the `/admin/deleteUser` pattern. Prior to Spring 5.3, this option is enabled by default.

On other systems, you may encounter discrepancies in whether `/admin/deleteUser` and `/admin/deleteUser/` are treated as distinct endpoints. In this case, you may be able to bypass access controls by appending a trailing slash to the path.
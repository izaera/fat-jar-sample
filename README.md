# Fat JAR PoC 

See https://issues.liferay.com/browse/LPS-132149 for the LPS.

This is a manually crafted example based on a standard JS Toolkit React portlet
project demonstrating how the Fat JAR feature could be implemented leveraging
the current bundler 2.

This repo is a Yarn workspace for demonstration purposes (i.e: so that it can be
built and deployed) but in the final image, only the 
[fat-test](tree/master/packages/fat-test) project would be necessary (user side)
because [liferay-7.4-GA1](tree/master/packages/liferay-7.4-GA1) would be 
published by us.

## Description of contents

-[fat-test](tree/master/packages/fat-test): this contains a React based portlet
 sample project as it would be seen by the user.
-[liferay-7.4-GA1](tree/master/packages/liferay-7.4-GA1): this contains a
 bundler preset with all necessary information to deploy a portlet to current
 liferay-portal (master). 

Things worth noting:

1) The `fat-test` project is a portlet because I started the PoC based on the 
   current state of the JS Toolkit, but the use case for the Fat JAR feature is
   (generally) not a portlet, but a Liferay extension project as those handled
   by `blade`.
2) Per the point avoid, we can assume that, most of the times, the projects like
   `fat-test` will be embedded a container Java project and that `blade` will be
   used to manage those.
3) Even though `liferay-7.4-GA1` is targeting the current master version of 
   `liferay-portal` I named it like that to show that we would have one of this
   per released Liferay version.
4) Per 3 above, bundler presets like `liferay-7.4-GA1` would really be the 
   equivalent of the fat JAR in the `npm` world.

I have tested that this works correctly in the current `liferay-portal` and that
it uses `react` from `frontend-js-react-web`.

Please read the commit history of the project to see the steps I made to
configure the project and the decissions taken.

Finally, note that this can be directly implemented with the current version of
the JS Toolkit (no need to change anything). However, we may want some minor 
modifications to be able to (for example):

- Use Babel 7
- Compile Soy
- Compile SAAS
- ...

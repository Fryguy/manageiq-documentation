You can change the maximum number of concurrent migrations for
conversion hosts or providers to control the impact of the migration
process on your infrastructure.

The provider setting has priority over the conversion host setting. For
example, if the maximum number of concurrent migrations is `20` for a
provider and `3` for five conversion hosts, the maximum number of
concurrent migrations is `20`, not `15` (`5` conversion hosts `x 3`
concurrent migrations per host).

An increase in the maximum number of concurrent migrations affects all
migration plans immediately. Virtual machines that are queued to migrate
will migrate in greater numbers.

A decrease maximum number of concurrent migrations affects only future
migration plans. Migration plans that are in progress will use the limit
that was set when the plan was created.

<div class="caution">

For VDDK transformation, the number of concurrent migrations must not
exceed `20`. Otherwise, network overload will cause the migration to
fail.

</div>

1.  Log in to the CloudForms user interface.

2.  Click **Compute** → **Migration** → **Migration Settings**.

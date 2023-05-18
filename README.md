# ansible-lint-test-role

This is a small example of an ansible-lint run failing on a role. To check this code, run:

    ansible-lint roles/test_role

Current output on ansible-lint v6.16.1 with ansible-core 2.15.0:

    WARNING  Listing 2 violation(s) that are fatal
    var-naming[no-role-prefix]: Variables names from within roles should use role_name_ as a prefix. (vars: __file__)
    roles/test_role/tasks/main.yml:9 Task/Handler: Failing task

    var-naming[no-role-prefix]: Variables names from within roles should use role_name_ as a prefix. (vars: __line__)
    roles/test_role/tasks/main.yml:9 Task/Handler: Failing task

The code that triggers these warnings is:

    - name: Failing task
      vars:
        test_role__var_check: true
      ansible.builtin.debug:
        msg: '{{ "Is the role working? " ~ test_role__var_check }}'

How should I deal with this?

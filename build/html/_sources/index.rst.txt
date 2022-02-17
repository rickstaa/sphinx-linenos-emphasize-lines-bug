.. sphinx-linenos-emphasize-lines-bug documentation master file, created by
   sphinx-quickstart on Thu Feb 17 11:31:43 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to sphinx-linenos-emphasize-lines-bug's documentation!
==============================================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:


.. code-block:: python
    :linenos:
    :emphasize-lines: 6, 12-14, 15, 17, 18-20

    import tensorflow as tf
    import os.path as osp

    from bayesian_learning_control.utils.log_utils.logx import EpochLogger

    from bayesian_learning_control.control.algos.tf2 import LAC

    MODEL_LOAD_FOLDER = "./data/lac/oscillator-v1/runs/run_1614673367"
    MODEL_PATH = osp.join(MODEL_LOAD_FOLDER, "tf2_save")

    # Restore the model
    config = EpochLogger.load_config(
        MODEL_LOAD_FOLDER
    )  # Retrieve the experiment configuration
    env = EpochLogger.load_env(MODEL_LOAD_FOLDER)
    model = LAC(env=env, ac_kwargs=config["ac_kwargs"])
    weights_checkpoint = tf.train.latest_checkpoint(MODEL_PATH)
    model.load_weights(
        weights_checkpoint,
    )

    # Create dummy observations and retrieve the best action
    obs = tf.random.uniform((1, env.observation_space.shape[0]))
    a = model.get_action(obs)
    L_value = model.ac.L([obs, tf.expand_dims(a, axis=0)])

    # Print results
    print(f"The LAC agent thinks it is a good idea to take action {a}.")
    print(f"It assigns a Lyapunov Value of {L_value} to this action.")


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

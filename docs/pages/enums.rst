Enums
-----

.. code-block:: python

   class RelayAction(IntEnum):
        """Possible relay actions."""
        MOMENTARY_ACTIVATION = 1
        LATCH = 2
        RELEASE = 3
        INQUIRY = 9


    class OptoAction(IntEnum):
        """Possible opto actions."""
        OFF = 0
        ON = 1
        INQUIRY = 9


    class SalvoOption(IntEnum):
        """Describes how salvos are organized."""
        ACTUAL_SALVO_NUM = 1
        ALPHANUMERIC_POSITION_OF_SALVO = 2


    class CrosspointTransitionControlSetting(IntEnum):
        """Possible transition control settings."""
        CUT_OUT_CUT_IN = 0
        CUT_OUT_FADE_IN = 1
        FADE_OUT_CUT_IN = 2
        FADE_OUT_FADE_IN = 3
        CROSS_FADE = 4
        CUT_OUT_CUT_IN_WITH_DSP = 9


    class FadeTime(IntEnum):
        """Possible fade times."""
        INSTANT = 0
        T_10MS = 1
        T_50MS = 2
        T_100MS = 3
        T_200MS = 4
        T_500MS = 5
        T_1S = 6
        T_2S = 7
        T_3S = 8
        T_4S = 9
        T_5S = 10
        T_6S = 11
        T_7S = 12
        T_8S = 13
        T_9S = 14
        T_10S = 15


    class GainChangeStage(IntEnum):
        """Possible gain change stages."""
        SOURCE_INPUT_SENSITIVITY = 1
        OUTPUT_GAIN_TRIM = 3
        DSP_COEFFICIENT_LEVEL_NO_FADE_TIME = 10
        DSP_COEFFICIENT_LEVEL_FADE_TIME = 11
        DSP_MIXER_OUTPUT_MASTER_LEVEL_NO_FADE_TIME = 15
        DSP_MIXER_OUTPUT_MASTER_LEVEL_FADE_TIME = 16


    class StereoLinkOption(IntEnum):
        """Describes if input or output should be modified."""
        INPUT_LINK = 0
        OUTPUT_LINK = 1


    class StereoLinkSetting(IntEnum):
        """Types of inputs and outputs."""
        MONO = 0
        STEREO = 1
        SOURCE_DEPENDENT = 2
        LR_MONO_SUM = 3


    class EnhancedTakeOptions:
        """Describes arguments for enhancement_take() method."""

        class PriorityLevel(IntEnum):
            """Possible priority levels."""
            STANDARD = 0
            IFB = 1

        class ControlOptions(IntEnum):
            """Possible control options."""
            OFF = 0
            ON = 1
            MOMENTARY = 2

        class ActionOptions(IntEnum):
            """Possible actions."""
            TAKE = 0
            SUM = 1
            DIRECT_RELAY_CONTROL = 2

        class SuppliedGainValueUsage(IntEnum):
            """Should use specified gain value."""
            NO = 0
            YES = 1

        class CurrentXpointTransitionCtlSpec(IntEnum):
            """Should use current xpoint transition control specification."""
            NO = 0
            YES = 1

        def __init__(self,
                     priority_level: PriorityLevel,
                     control_options: ControlOptions,
                     action_options: ActionOptions,
                     use_supplied_gain_value: SuppliedGainValueUsage,
                     use_current_xpoint_transition_ctl_spec: CurrentXpointTransitionCtlSpec
                     ):
            self.value = int(priority_level)
            self.value += int(control_options) << 2
            self.value += int(action_options) << 5
            self.value += int(use_supplied_gain_value) << 9
            self.value += int(use_current_xpoint_transition_ctl_spec) << 10

        def get(self):
            """
            Get calculated enhanced take command options numeric value.
            :return: value calculated for arguments provided in constructor.
            """
            return self.value


    class ConsoleModuleAction(IntEnum):
        """Possible console module actions."""
        TURN_MODULE_OFF_WITH_SOURCE_SELECTED = 0
        TURN_MODULE_ON_WITH_SOURCE_SELECTED = 1
        TURN_CUE_OFF_ON_MODULE_WITH_SOURCE_SELECTED = 2
        TURN_CUE_ON_ON_MODULE_WITH_SOURCE_SELECTED = 3


    class AlphanumericNameInquiryInputOutput(IntEnum):
        """Alphanumeric name inquiry should be shown for input or output."""
        INPUT = 0
        OUTPUT = 1


    class FeedbackReplies(IntEnum):
        """Feedback replies should be enabled or disabled."""
        ENABLED = 1
        DISABLED = 0


    class FeedbackTally(IntEnum):
        """Possible feedback tally options."""
        NO_TALLY_OF_XPOINT_ACTIVITY_OR_ALPHA_CHANGE_NOTIFICATION = 0
        XPOINT_TALLY_IN_NUMERICAL_FORMAT_ONLY = 1
        XPOINT_TALLY_AS_CHANNEL_ALPHA_LABELS_ONLY = 2
        XPOINT_TALLY_BOTH_NUMERICAL_AND_ALPHA_LABELS = 3
        NOTIFICATION_OF_CHANGES_TO_THE_ALPHA_LABELS = 4
        NUMERICAL_TALLY_AND_ALPHA_CHANGE_NOTIFICATION = 5
        ALPHA_LABEL_TALLY_AND_ALPHA_CHANGE_NOTIFICATION = 6
        NUMERICAL_AND_ALPHA_LABEL_TALLY_WITH_ALPHA_CHANGE_NOTICE = 7
        NOTICE_OF_CONSOLE_MODULE_OPERATIONS_ONLY = 8
        NOTICE_OF_CONSOLE_MODULE_OPERATIONS_AND_NUMERICAL_TALLY_AND_ALPHA_CHANGE_NOTIFICATION = 9


    class FeedbackProtocol(IntEnum):
        """Possible feedback variants."""
        THREE_DIGIT_ASCII_STYLE_XPOINT_TALLY = 0
        TWO_DIGIT_ASCII_HEX_STYLE_XPOINT_TALLY = 1
        FOUR_DIGIT_ASCII_STYLE_XPOINT_TALLY = 2


    class Reply(IntEnum):
        """Default replies."""
        OK = 0
        ERROR = 1